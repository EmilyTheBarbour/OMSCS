**Stands for Instruction Level Parallelism

- Allows executing multiple *instructions* simultaneously 

There are many forms of ILP:
* [[Super Scalars]]
- [[VLIW]]
- [[In Order Processors]]
- [[Out of Order Processors]]

You can combine ordering and instruction makeup, i.e 
- Super Scalar, In order
- Super Scalar, out of order
- VLIW, In order
- VLIW, out of order

Example 5 Stage [[Pipelines]]: 
![[Pasted image 20230826145301.png]]
* IF -> Instruction Fetch
* ID -> Instruction Decode
* EX -> Execute
* MEM -> Memory Access (to get operands)
* WB -> Write Back (write back to memory)

The level of ILP able to be taken advantage of is a property of the running program
- some programs are able to have a higher level of ILP than others 

Independent of Hardware Technology Improvements
- I.E [[Clock Frequency]], Memory, etc.