Reduced Instruction Set Computer

Classic RISC [[Pipelines]] are 5 stage:
1. `IF`: Instruction Fetch
	- Get the next instruction from the cache
1. `ID`: Instruction Decode
	- Decode the instruction to get what it actually is
2. `EX`: Execute
	- perform [[ALU]] operation **OR** address calculation in a memory op
3. `MEM`: Memory Access
	- If the operation has memory op, access the referenced memory
4. `WB`: Write Back
	- result of the operation are written back, either to memory or registers

![[Pasted image 20230826145301.png]]