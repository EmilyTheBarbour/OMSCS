Three types that indicate, based on program construction, whether an instruction is dependent on data resultant from another instruction. 

1. Read-After-Write (RAW): True Dependency

![[Pasted image 20230826164637.png]]
- Data in R1 is required in instruction B, but instruction A computes R1 through R2 and R3.

2. Write-After-Write (WAW): False Dependency

![[Pasted image 20230826164815.png]]
-  A first writes to R1, then B writes to R1. 

3. Write-After-Read (WAR): False Dependency

![[Pasted image 20230826164947.png]]
- Instruction A is reading data, so Instruction B cannot override it until A is complete.