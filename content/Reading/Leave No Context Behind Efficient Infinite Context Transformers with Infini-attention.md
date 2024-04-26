# Abstract
This work introduces an efficient method to scale Transformer-based Large Language Models (LLMs) to infinitely long inputs with bounded memory and computation. A key component in our proposed approach is a new attention technique dubbed Infini-attention. The Infini-attention incorporates a compressive memory into the vanilla attention mechanism and builds in both masked local attention and long-term linear attention mechanisms in a single Transformer block. We demonstrate the effectiveness of our approach on long-context language modeling benchmarks, 1M sequence length passkey context block retrieval and 500K length book summarization tasks with 1B and 8B LLMs. Our approach introduces minimal bounded memory parameters and enables fast streaming inference for LLMs.

# By
Google engineers.
# Takeaways
They combine a local attention window (e.g. last 1000 tokens) with essentially a long term memory. The long term memory can be thought of as the result of a reduce operation on all previous local attention windows. Allowing the model to attend to both near and far information (with learnt parameters for how important either is) while having a bounded memory usage (size of the long term memory and the local window).

Memory is definitely linear, compute looks like it'd be linear but not 100% sure.

What does it mean, future AI models could have much larger contexts without the same scaling issues.