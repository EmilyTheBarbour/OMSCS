Keep executing instructions, but tag their commit with the branch outcome. This is done by holding back execution of the instruction in the last stage of the pipeline (for example `WB` in [[RISC]]), and waiting until the branch condition is known. Those that match the tagged value of the branch will execute their last stage of the pipeline and commit.

e.g [[Conditional Move]]