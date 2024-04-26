# Abstract
Natural language understanding comprises a wide range of diverse tasks such
as textual entailment, question answering, semantic similarity assessment, and
document classiﬁcation. Although large unlabeled text corpora are abundant,
labeled data for learning these speciﬁc tasks is scarce, making it challenging for
discriminatively trained models to perform adequately. We demonstrate that large
gains on these tasks can be realized by generative pre-training of a language model
on a diverse corpus of unlabeled text, followed by discriminative ﬁne-tuning on each
speciﬁc task. In contrast to previous approaches, we make use of task-aware input
transformations during ﬁne-tuning to achieve effective transfer while requiring
minimal changes to the model architecture. We demonstrate the effectiveness of
our approach on a wide range of benchmarks for natural language understanding.
Our general task-agnostic model outperforms discriminatively trained models that
use architectures speciﬁcally crafted for each task, signiﬁcantly improving upon the
state of the art in 9 out of the 12 tasks studied. For instance, we achieve absolute
improvements of 8.9% on commonsense reasoning (Stories Cloze Test), 5.7% on
question answering (RACE), and 1.5% on textual entailment (MultiNLI).

# Snippets
We employ a two-stage training procedure. First, we use a language modeling objective on
the unlabeled data to learn the initial parameters of a neural network model. Subsequently, we adapt
these parameters to a target task using the corresponding supervised objective.

For our model architecture, we use the Transformer [62], which has been shown to perform strongly on
various tasks such as machine translation [62], document generation [34], and syntactic parsing [29].
This model choice provides us with a more structured memory for handling long-term dependencies in
text, compared to alternatives like recurrent networks, resulting in robust transfer performance across
diverse tasks.

# Takeaways
Generative pre-training gives a model a strong base understanding of the language.

Generative = Unsupervised training where it tries to generate the next word based on unlabelled data
Pre-training - Learn the raw structure of the language itself from data scraped from various sources.