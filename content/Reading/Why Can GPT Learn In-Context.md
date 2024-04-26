# Abstract
Large pretrained language models have **shown surprising in-context learning** (ICL) ability. **With a few demonstration input-label pairs, they can predict the label for an unseen input without parameter updates.** Despite the great success in performance, its working mechanism still remains an open question. In this paper, **we explain language models as meta-optimizers and understand in-context learning as implicit finetuning**. Theoretically, we figure out that Transformer attention has a dual form of gradient descent. On top of it, we understand ICL as follows: GPT first produces meta-gradients according to the demonstration examples, and then these meta-gradients are applied to the original GPT to build an ICL model. We comprehensively compare the behaviors of in-context learning and explicit finetuning on real tasks to provide empirical evidence that supports our understanding. Experimental results show that in-context learning behaves similarly to explicit finetuning from multiple perspectives. Inspired by the dual form between Transformer attention and gradient descent, we design a momentum-based attention by analogy with gradient descent with momentum. The improved performance over vanilla attention further supports our understanding from another perspective, and more importantly, shows the potential to utilize our understanding for future model design. The code is available at \url{https://aka.ms/icl}

# Extracts
Transformer-based architectures (e.g.,
GPT; Brown et al. 2020), have shown strong emer-
gent in-context learning (ICL) ability (Wei et al.,
2022; Dong et al., 2023). Different from finetuning
which needs additional parameter updates, ICL just
needs several demonstration examples prepended before the query input, and then the model can pre-
dict labels for unseen inputs.

![[Pasted image 20240331145345.png]]

# Key Takeaways
In context learning (ICL) e.g. few shot has similar or better performance to just fine-tuning. Which means that I should include examples in the system prompt and not waste resources on fine tuning the model for the task of specification generation.