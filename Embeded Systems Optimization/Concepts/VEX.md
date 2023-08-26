Implements a different level of ILP called [[VLIW]]

- there is only one memory operation allowed in each slot
	- Only 1 memory unit available in the processor
- Allows [[Dismissable Loads]] `ldw.d`
	- Independent loads are *hoisted* above branches