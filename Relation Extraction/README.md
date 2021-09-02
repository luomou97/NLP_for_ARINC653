## Why using IE tool to extract relation?
Traditional RE (relation extraction) tools have two potential disadvantages:
1. the relation types are predefined and limited (such as [OpenNRE](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fthunlp%2FOpenNRE&sa=D)) which will affect the correctness and integrity of relation extraction;
2. RE tools pay major attention to the relation between entity-pair but ignore the modifier of entities, such as "specified process is in the DORMANT state" will be parsed into <process, in, DORMANT state> but discard the important modifier "specified".

Besides, ARINC653 P1-5 only has the content of 300 pages (including graphics, table and catalogue),  which has no comparable scale to the corpus (e.g, [biomedicine](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fshangjingbo1226%2FAutoNER&sa=D), new reports, etc.). However, [OpenIE4](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fallenai%2Fopenie-standalone&sa=D) can solve the above problems well.

Based on our IEMerger algorithm with the output of OpenIE4, we can successfully extract the desired relations and reach a high (over 97%) performance for all three ARINC653 versions (P1-3 to P1-5). 
![image](https://github.com/luomou97/NLP_for_ARINC653/blob/main/Relation%20Extraction/Algo2_1.jpg)

