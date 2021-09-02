## Process Attribute Definition
2. **Deadline Time**  – Defines the absolute system time when a process will exceed its deadline. The deadline time is evaluated by the operating system to determine whether a process is satisfactorily completing its processing within the allotted time. When a process is dormant (i.e., stopped), the deadline time returned by GET_PROCESS_STATUS is undefined.

……

7. **Deadline** – Specifies the type of deadline relating to a process and may be “hard” or “soft.” When a process fails to meet its deadline, the O/S does not react differently between “hard” and “soft” deadlines. The O/S will take the action defined for deadline missed defined in the HM tables. If a process level error handler is defined, the process level error handler can utilize the GET_PROCESS_STATUS service to obtain the deadline type and take application-specific actions based on “hard” versus “soft” deadlines.

```
1  procedure REPLENISH
2    (BUDGET_TIME		:	in SYSTEM_TIME_TYPE;
3    RETURN_CODE		:	out RETURN_CODE_TYPE) is
4  error
5    when (process is error handler process or operating mode is not NORMAL) =>
6      RETURN_CODE := NO_ACTION;
7    when (current process is periodic and new deadline will exceed next release point) =>
8      -- an infinite BUDGET_TIME will always exceed the next release point
9      RETURN_CODE := INVALID_MODE;
10  when (BUDGET_TIME is out of range) =>
11    -- e.g., calculation causes overflow of underlying clock
12    RETURN_CODE := INVALID_PARAM;
13 normal
14  set a new DEADLINE_TIME value for the current process to (current system clock + BUDGET_TIME);
15  -- if current process’s TIME_CAPACITY is infinite or BUDGET_TIME is
16  -- infinite then the DEADLINE_TIME is infinite,
17  -- i.e., there is no effective deadline
18  RETURN_CODE := NO_ERROR;
19 end REPLENISH;
```
As the process attribute definition above, ***deadline time***, the actual execution  time of process, is not identical  to another  enum variable ***deadline***. However, in the error part of pseudocode REPLENISH, it doesn't distinguish them and treat them as the same mistakenly. 
## Hidden danger
Assume that, during the implement of ARINC653 OS and you have already defined the two attributes (**named deadline_time and deadline respectively**) for process, when implementing the REPLENISH API and encountering the red statement, we are much likely to directly `code as "if (this->process.deadline > next(release point))"` **(the 7th line code)**. Catastrophically, it will not report any Compile Error or Run Error (**in C language, an enum value is an alias of one integer**), continues to execute **without returning INVALID_MODE error**, which definitely laies a lot of hidden dangers especially for such industrial aviation OS.

Besides, this inconsistency issue is still legacy in the latest version (ARINC653 P1-5), and **we found there exist more than 20 instances of this issue across different formats (plain text, pseudocode)**. Thus, we have reported this issue to ARINC653 standard committee. 

Detailed issues:
- It is expected that at the end of each processing cycle a process will call the PERIODIC_WAIT service to get a ***new deadline***. The ***new deadline*** is calculated from the next periodic release point for that process.
- A time-out delay or ***deadline*** can expire outside the partition window. It is acted upon at the beginning of the next partition window.
- Failure to invoke a 2nd PERIODIC_WAIT before the ***deadline associated with the process***’ next period results in another deadline miss HM event.
- expiration of a ***process’ deadline*** does not affect the process’ period
- Dependencies between ***process deadline*** and the partition time windows include whether a partition’s duration is divided into multiple time windows
- When a process is started (either explicitly via a service request or at the end of the initialization phase), its ***deadline*** is set to the value of current time plus time capacity
- Time capacity is associated with periodic and aperiodic processes and is used to set ***process deadline***. The ***deadline associated with a blocked process*** will continue to be evaluated while it is blocked. The ***deadline associated with periodic processes*** is reset by invoking the PERIODIC_WAIT service. The ***deadline associated with aperiodic processes*** is reset by using the stop and start services.
