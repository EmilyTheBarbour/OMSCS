- [x] Complete Lecture 📅 2023-08-27 ✅ 2023-08-26
### Core concepts 

| Concepts |                         |            |                               |                             |                     |                       |
| -------- |:----------------------- | ---------- | ----------------------------- | --------------------------- | ------------------- |:--------------------- |
| [[ALU]]  | [[Branches]]            | [[Bubble]] | [[Clock Frequency]]           | [[Control Dependencies]]    | [[Control Hazards]] | [[Dismissable Loads]] |
| [[ILP]]  | [[In Order Processors]] | [[IPC]]    | [[Long Latency Instructions]] | [[Out of Order Processors]] | [[Pipeline Flush]]  | [[Pipelines]]         |
| [[RISC]] | [[Super Scalars]]       | [[VEX]]    | [[VLIW]]                      |     [[Data Dependencies]]                        |   [[Speculation]]                  |      [[Register Renaming]]                 |
### Embeded Systems Are different

*3 key goals of embeded systems:
- Low Power
- High Performance
- Low Cost

![[Pasted image 20230826144135.png]]

[[VLIW]], [[In Order Processors]] are the most preferred design choice for embedded processors. 
- Multiple Instructions in a slot lead to better performance
- In order, with instruction level parallelism also lowers energy cost
## [[ILP]] in Embeded Systems
- Can *save power* by exploiting more ILP, which can lead to decreasing required clock speeds

Typical [[Pipelines]] in modern high performance processors are 15-20 stages.
- Pentium 4 (last non-multicore) had 20 stage pipeline
- Sandy bridge / Haswell had 14 stage pipeline

*why have processors moved to scale down their pipeline over time?*

## Sequential Program Semantics

![[Pasted image 20230826150429.png]]

Typically in every clock cycle, you can expect the execution of 1 instruction per cycle.
- in *reality*, many instructions take more than one cycle to complete
	- For example, **LOAD**s and **BRANCH**es are notorious for taking more than 1 cycle
- In a *Sequential* program, you **MUST** wait for the previous instruction to complete before you start execution of the next instruction

In the above Example:
- `add a, b, c` has to pause for 2 cycles because:
	- The value of `a` is not available until the `WB` of `mov a, 15`
	- the value of `b` is not available until the `WB` of `mov b, 20`
	- Note however, that we were able to still execute `IF` and `ID` as they are not dependent on anything else. 

In general, the semantics in a *single thread:*
1. processor tries to issue an instruction every clock cycle
	- But, there are [[Control Dependencies]], [[Control Hazards]], [[Long Latency Instructions]]
	- Delays result in execution of < 1 instruction per cycle, on average

## How Can we obtain ILP?

* Roughly, by [[IPC]]
	* Strict Sequential Semantics offer a low IPC
		* mainly due to instructions being *stalled* for data or resource release by other instructions
	* Keeping pipelines full allows us to maximize usage, and achieve near IPC ~= 1

## Non-pipelined Example using [[VEX]]

```VEX
ldw $r20 = 0[$r20]
nop
nop
cmpeq $b0 = $r20, 0
nop
br $b0, DONE
ldw $r23 = 0[$r13]
nop
nop
sub $r23 = $r23, $r20
add $r4 = $r4, $r23
```

- What are the purpose of the `NOP`?
	- Add a delay to the pipeline, so that instructions can complete
- `LDW` (load) instructions take up to 3 cycles, since data may not be present in a cache
	- Similarly, `CMP` instructions take 2 cycles

Using [[Dismissable Loads]] as mentioned in [[VEX]]:
- load `B0` takes 3 cycles, which requires 2 `NOP`
- 2 additional loads (`B1` and `B2`) are inserted into `[2]` and `[3]` slots. These are Dismissible. 
### Instructions Above Mapped to Clock Cycles

| Clock Cycle | Instruction |
| ----------- | ----------- |
| 1           |             |
| 2           | `loadw`       |
| 3           |             |
| 4           | `cmpeq`       |
| 5           |             |
| 6           | `br`          |
| 7           | `loadw`       |
| 8           |             |
| 9           |             |
| 10          | `sub`         |
| 11          | `add`            |

$IPC = 6 / 11 \rightarrow 0.55$

## IPC Quiz

![[Pasted image 20230826153412.png]]

Let:
$L = 5$, $S = 4$, $R = 4$, $B = 3$, $J = 3$, $O = 0$

For the given program:
$0.5R + 0.1L + 0.2S + 0.08B + 0.02J + 0.1O = CPI$
$0.5(4) + 0.1(5) + 0.2(4) + 0.08(3) + 0.02(3) + 0.1(0) = CPI$
$2 + 0.5 + 0.8 + 0.24 + 0.06 + 0 = CPI$
$3.6 = CPI$

Each instruction, on average, takes **3.6 cycles** to execute in this program.

## Minimizing Dependencies

2 different types of dependencies:
- [[Control Dependencies]]
- [[Data Dependencies]]

There are many techniques to try and minimize the impact of dependencies
- [[Speculation]]
- [[Predication]]
- [[Register Renaming]]
	- Particularly related to [[Data Dependencies]]

## Other Parallelisms
- [[Vector Processing]]
	- **Rarely used for Embedded Systems**
- [[Multithreading and Multiprocessing]]
	- **approach has to be cautiously applied for embeded processors**
- [[Micro-SIMD]]
	- **Slowly being adopted in embedded processors**