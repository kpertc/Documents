> [CS 194/294-196 (LLM Agents)- Lecture 1, Denny Zhou](https://www.youtube.com/watch?v=QL-FS_Zcmyo&list=PLGK6tAsp1smbj8Ga4JHcgzGNbXArity-c)

- Intermediate steps
	- Training / fineTuning / prompting with intermediate steps (Chain of Thought, COT)
	- Zero-shot, analogical reasoning (LLM generates its own examples first), special decoding (CoT-decoding: look at top-k alternatives at the first token instead of greedy)
- Self-Consistency
	- generate multiple independent responses to the same prompt and then selecting the most consistent or prevalent answer
- Limitation
	- LLMs can be easily distract from ==irrelevant content==
	- Self correct: (worse than self-consistency method) LLMs can correct inaccurate answers, ==may also risk changing correct answers into in correct ones==
	- Content (questions) order matters

Define a right problem to work on

Zero-shot: You give no examples in the prompt
One-shot: You give one example, then ask the model
Many-shot: hundreds~thousands of examples in context (needs long context), can rival fine-tuning on some tasks

prompt engineering guide
- https://platform.openai.com/docs/guides/prompt-engineering
- https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview

[CS 194/294-196 (LLM Agents) - Lecture 3, Chi Wang and Jerry Liu](https://www.youtube.com/live/OOdtmCMSOo4?si=y9EcKGGYIGAv-eLn)

Agent → Handle more complex tasks, improve response quality

Compound AI system

framework:
	- AutoGen (v0.4 rewrite; now folded with Semantic Kernel into Microsoft Agent Framework)
	- LangChain [[LangChain]] [[LangChain.js]], LangGraph (the stateful/agent part)

Meta-prompting → LLMs generate, modify, or optimize prompts for themselves

Evaluate Performance
- data sets
- good LLMs, e.g. GPT5-high