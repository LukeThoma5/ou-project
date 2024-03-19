---
date: 2024-02-27
week: 9
---
Date: Tuesday, February 27, 2024
# Work Undertaken Summary
TMA work mostly. See time spent.
Investigate Grounding vs FineTuning AI models.


# Time Spent
- 1.75hrs risk register
- 0.5hr microsoft grounding paper.
- 0.35hr on stack overflow llm blogpost.
- 0.35 logbook deployment.
- 25 minutes project schedule
- 10 minutes tutor email
- 25 minutes ollama langchain
- 1.35 hrs on literature search
- 1.25 hrs 1.58 bit llm paper
- 1 hr on TMA
- 1 hr on Mendeley and importing all my references
- 15 minutes OU resources
- 4.75 hours on TMA01
- 7 hours on TMA01
# Questions for Tutor
N/A

# Next work planned
Review course on NLP - [Introduction (huggingface.co)](https://huggingface.co/learn/nlp-course/chapter1/1#who-are-we)
Review RAG as described by langchain [Deconstructing RAG (langchain.dev)](https://blog.langchain.dev/deconstructing-rag/)


# Raw Notes

# Risk Assessment
![[2024-02-21 and -02-26 - TMA01 Execution#Risk Assessment]]


# Skills required
## Owned skills
- Python
- Linux Administration
- Docker
- Pandas
- Seaborn
- C#
- Entity Framework
- Sql Server
- Html
- Networking
- Project Management
## Requiring refinement
- LangChain - LangChain Docs
- Ollama - Ollama docs
- Prompt Engineering - Literature Search

# Resources Required
- LangChain documentation
- Ollama Documentation
- User Story Database - Backup from live database (we use our own)
- Server with GPU with sufficient video memory (24GB) AMD 7900 XTX
- No other people - I am the primary stakeholder and capable of judging the output.
- OU library
- Hugging Face (AI development knowledge base)
- LLM Models - Downloaded from ollama

## TODO
- [x] Install mendeley for tracking my references.  [How to add references into word using google scholar and mendeley (youtube.com)](https://www.youtube.com/watch?v=cGA6oqGzh4Y&t=130s)
- [x] Rewatch the video with the section on risks. To ensure we create something good.
- [x] DO I need to do some literature search before TMA01?


# Research - Grounding and fine-tuning

review this [Grounding LLMs - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/grounding-llms/ba-p/3843857)

fine-tuning vs grounding? Difference?
[Grounding LLMs - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/grounding-llms/ba-p/3843857)

fine-tuning is properly adding the data into the memory of the model? While grounding is adding information to the context at runtime to help it produce an answer.

# [Even LLMs need education—quality data makes LLMs overperform - Stack Overflow](https://stackoverflow.blog/2024/02/26/even-llms-need-education-quality-data-makes-llms-overperform/)
Article talks about how a smaller model grounded in domain data can punch above its weight compared to a very large model.

It suggests that a smaller LLM (7B params) with effective RAG is a cost effective path. Even better to combined fine-tuning and RAG. So maybe I should fine-tune with all the data and then try to incrementally add the current version with RAG.

I might end up comparing RAG vs RAG+fine tuning for a single model.

Might want to try a different generation technique where I put all the documentation into an embeddings and then just feed the model that and a topic heading and let it generate the whole topic at once?

It seems like yes the input and the output all need to fit within the context window. Yikes...

# 1.58bit llm
#research The Era of 1-bit LLMs: All Large Language Models are in 1.58 Bits
[https://arxiv.org/pdf/2402.17764.pdf](https://arxiv.org/pdf/2402.17764.pdf) new paper by microsoft. "the 1.58 bit LLM". Essentially rather than using 16-bit floating points for the model weights/parameters, they use a tri-state {-1, 0, 1}. Which ends up averaging out at 1.58 bits per parameter. This means rather than matrix floating point multiplication its (mostly) just integer addition. Past 3B parameters the two methods have similar reasoning / effectiveness. With the 1.58bit llm at 70B parameters using 7x less ram, 9x the token throughput and 40x less energy than the same model size using 16-bit floats.

Takeaways: more cost effective AI, easier to deploy AI (less memory footprint, more CPU friendly)

# [[2402.17463] Training-Free Long-Context Scaling of Large Language Models (arxiv.org)](https://arxiv.org/abs/2402.17463)

Methods for increasing context length without having to spend a lot of time fine tuning for greater context.

## Design choices
Because of the context window, going to need to generate the specification in parts. E.g. Application, Cases, Leads etc.

Have on each iteration it spit out the result to file and then take a commit. So each run of the LLM is a branch and we just keep adding commits so we can see how it evolves.


# Ollama Docs
[langchain_community.llms.ollama.Ollama — 🦜🔗 LangChain 0.1.9](https://api.python.langchain.com/en/latest/llms/langchain_community.llms.ollama.Ollama.html#langchain_community.llms.ollama.Ollama)
[langchain_community 0.0.24 — 🦜🔗 LangChain 0.1.9](https://api.python.langchain.com/en/latest/community_api_reference.html#module-langchain_community.llms)
[Ollama | 🦜️🔗 Langchain](https://python.langchain.com/docs/integrations/llms/ollama)

# Checklist
- a.Identifying the goals and content of your project.
- b.Starting to select and evaluate relevant information sources that describe related work and point to possible methods to be used.
- c.Identifying resources (especially data, access to people, etc.) that are crucial for success and assured yourself that these will be available when needed.
- d.Identifying and evaluating your own skills and knowledge that are crucial for the success of this project. Identifying essential skills that you lack and starting to develop them.
- e.Choosing an appropriate project lifecycle model and starting to plan and schedule the work required based upon this.
- f.Undertaking some exploratory work to begin the project work.
- g.Reflect on progress to date.