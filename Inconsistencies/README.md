## Process Attribute Definition
2. **Deadline Time** – Defines the absolute system time when a process will exceed its deadline. The deadline time is evaluated by the operating system to determine whether a process is satisfactorily completing its processing within the allotted time. When a process is dormant (i.e., stopped), the deadline time returned by GET_PROCESS_STATUS is undefined.

……

7. **Deadline** – Specifies the type of deadline relating to a process and may be “hard” or “soft.” When a process fails to meet its deadline, the O/S does not react differently between “hard” and “soft” deadlines. The O/S will take the action defined for deadline missed defined in the HM tables. If a process level error handler is defined, the process level error handler can utilize the GET_PROCESS_STATUS service to obtain the deadline type and take application-specific actions based on “hard” versus “soft” deadlines.

```
procedure REPLENISH
  (BUDGET_TIME		:	in SYSTEM_TIME_TYPE;
  RETURN_CODE		:	out RETURN_CODE_TYPE) is
error
  when (process is error handler process or operating mode is not NORMAL) =>
    RETURN_CODE := NO_ACTION;
  when (current process is periodic and new deadline will exceed next release point) =>
    -- an infinite BUDGET_TIME will always exceed the next release point
    RETURN_CODE := INVALID_MODE;
  when (BUDGET_TIME is out of range) =>
    -- e.g., calculation causes overflow of underlying clock
    RETURN_CODE := INVALID_PARAM;
normal
  set a new DEADLINE_TIME value for the current process to (current system clock + BUDGET_TIME);
  -- if current process’s TIME_CAPACITY is infinite or BUDGET_TIME is
  -- infinite then the DEADLINE_TIME is infinite,
  -- i.e., there is no effective deadline
  RETURN_CODE := NO_ERROR;
end REPLENISH;
```
