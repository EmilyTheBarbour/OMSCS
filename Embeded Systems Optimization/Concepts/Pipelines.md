Technique for implementing [[ILP]] with a single processor by attempting to keep every part of the processor busy by separating instructions into sub instructions, and having the ability to run one of each simultaneously

Example of classic [[RISC]] 5 stage pipeline:

![[Pasted image 20230826145301.png]]

- A later operation can *share the resource* used by the first operation in previous cycles
- Shared hardware can be pipelined
	- For example, **Integer Multiplier** is pipelined

for a $k$ sized pipeline, the $n$th stage of the pipeline will initially not have anything to execute for $n-1$ cycles. Therefore, for a $k$ stage pipeline, it takes $k-1$ cycles to fill up all the stages at the beginning of execution.
