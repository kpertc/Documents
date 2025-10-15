> [CS 194/294-196 (LLM Agents)- Lecture 1, Denny Zhou](https://www.youtube.com/watch?v=QL-FS_Zcmyo&list=PLGK6tAsp1smbj8Ga4JHcgzGNbXArity-c)

- Intermediate steps
	- Training / fineTuning / prompting with intermediate steps (Chain of Thought, COT)
	- Zero-shot, analogical reasoning (show LLMS examples), special decoding (Greedy Decoding)
- Self-Consistency
	- generate multiple independent responses to the same prompt and then selecting the most consistent or prevalent answer
- Limitation
	- LLMs can be easily distract from ==irrelevant content==
	- Self correct: (worse than self-consistency method) LLMs can correct inaccurate answers, ==may also risk changing correct answers into in correct ones==
	- Content (questions) order matters

Define a right problem to work on 


[CS 194/294-196 (LLM Agents) - Lecture 3, Chi Wang and Jerry Liu](https://www.youtube.com/live/OOdtmCMSOo4?si=y9EcKGGYIGAv-eLn)

Agent → Handle more complex tasks, improve response quality
framework:
	- AutoGen
	- LangChain

Meta-prompting → LLMs generate, modify, or optimize prompts for themselves