# Abstract
We demonstrate that scaling up language models greatly improves task-agnostic, few-shot performance, sometimes even becoming competitive with prior state-ofthe-art fine-tuning approaches. Specifically, we train GPT-3, an autoregressive language model with 175 billion parameters, 10x more than any previous nonsparse language model, and test its performance in the few-shot setting. For all tasks, **GPT-3 is applied without any gradient updates or fine-tuning**, with tasks and few-shot demonstrations specified purely via text interaction with the model. GPT-3 achieves strong performance on many NLP datasets, including translation, question-answering, and cloze tasks. We also identify some datasets where GPT3’s few-shot learning still struggles, as well as some datasets where GPT-3 faces methodological issues related to training on large web corpora

# Snippets
NLP has shifted from learning task-specific representations and designing task-specific architectures to using task-agnostic pre-training and task-agnostic architectures

![[Pasted image 20240331153407.png]]

The dramatic increase from 0 to 1 examples for In-context learning.

We observe that one- and few-shot performance is often much higher than true zero-shot performance leading us to suggest that language models can also be understood as meta-learners where slow outer-loop gradient descent based learning is combined with fast “in-context” learning implemented within the context activations of the model.

Broadly, on NLP tasks GPT-3 achieves promising results in the zero- and one-shot settings, and in the few-shot setting is sometimes competitive with or even occasionally surpasses state-of-the-art (fine tuned).

**Fine-Tuning** (FT) - updates the weights of a pre-trained model by training on thousands of supervised labels specific to the desired task. The main advantage of fine-tuning is strong performance on many benchmarks. The main **disadvantages** are the **need for a new large dataset for every task, the potential for poor generalization out-of-distribution** [MPL19], and the potential to exploit spurious features of the training data [GSL+18, NK19]. We focus on task-agnostic performance, leaving fine-tuning for future work.

**Few-Shot** (FS) - the model is given a few demonstrations of the task at inference time as conditioning [RWC+19], but no weights are updated. An example typically has a context and a desired completion (for example an English sentence and the French translation), and few-shot works by giving K examples of context and completion, and then one final example of context, with the model expected to provide the completion (see appendix for more details). We typically set K in the range of 10 to 100, as this is how many examples can fit in the model’s context window (nctx = 2048). The main advantage of few-shot is a major reduction in the need for task-specific data. The main disadvantage is that results from this method have so far been much worse than state-of-the-art fine-tuned models. Also, a small amount of task specific data is still required. As indicated by the name, few-shot learning as described here for language models is related to few-shot learning as used in other contexts in ML [HYC01, VBL+16] – both involve learning based on a broad distribution of tasks and then rapidly adapting to a new task.

• **One-Shot** (1S) - similar to few-shot but with K = 1.
• **Zero-Shot** (0S) - similar to few-shot but with a natural language description of the task instead of any examples.

# Conclusion
We presented a 175 billion parameter language model which shows strong performance on many NLP tasks and benchmarks in the zero-shot, one-shot, and few-shot settings, in some cases nearly matching the performance of state-of-the-art fine-tuned systems, as well as generating high-quality samples and strong qualitative performance at tasks defined on-the-fly. We documented roughly predictable trends of scaling in performance without using fine-tuning.

# Key Takeaways
- Paper introduces GPT-3
- few shot general models are competitive with fined-tuned SOTA models

# Also useful
Paper also discusses impacts of good large language models as well as gender and race bias.
Potential issues with scammers/spammers and issues around energy use
![[Pasted image 20240331161329.png]]
