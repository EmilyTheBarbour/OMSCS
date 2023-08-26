One of the major sources of IPC degradation 

At the point of a branch, you can't easily determine which instruction path you should start loading into your [[Pipelines]].

There is a chance that you load instructions into the pipeline, but the conditions for the branch cause you to take a different path, requiring you to nullify what was loaded into the pipeline. This will induce a latency as you now have to load the other code path.

- Uncertain Paths cause a [[Bubble]] in the pipeline
- Wrong paths incur a large penalty of a [[Pipeline Flush]]
Easiest way to handle this is to purposely put a bubble or a delay to wait until the branch is resolved.

Independent operations could instead be computed where a delay would originally be inserted so as to utilize otherwise wasted time.

Realistically, its hard to move a branch up much, if at all, and often you can't find enough operations / instructions to fill up all the required slots.


![[Pasted image 20230826161106.png]]