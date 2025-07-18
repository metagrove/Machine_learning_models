Transformer From Scratch
A step-by-step Transformer implementation with full PyTorch code, but with enough firepower to melt your GPU. 💥

🧱 What’s Inside?
This repo contains everything you need to understand and build a Transformer from scratch using PyTorch. No TensorFlow. No Keras. No pre-trained cheating. Just raw brainpower and code.

📦 File: transformer_from_scratch.py
🔥 Components, Explained Like You're 5 (or 50, with coffee)
1. 🎫 TokenEmbedding
"I turn boring word IDs into juicy dense vectors."


class TokenEmbedding(nn.Module):
    def __init__(self, vocab_size, embed_size):
        self.embedding = nn.Embedding(vocab_size, embed_size)

    def forward(self, x):
        return self.embedding(x)
When you say “I love cats,” the model only sees [6, 12, 99]. Embedding turns those IDs into actual vectors the model can work with — like giving it glasses to see meanings.

2. 🧭 PositionalEncoding
"Because ‘I love you’ is different from ‘You love I’..."

class PositionalEncoding(nn.Module):
    ...
Transformers don’t have RNNs to remember order, so we add sine & cosine waves to embed position info directly into the token vectors. Yes, we're literally adding trig functions to English sentences. 🎢

3. 🧠 MultiHeadSelfAttention
"Every word gets to eavesdrop on every other word — but in parallel."


class MultiHeadSelfAttention(nn.Module):
    ...
Query, Key, Value: Like a school of spies 🕵️‍♀️ — each word asks questions (Q), gives answers (K), and delivers content (V).

Heads: Multiple “views” of the same room. One head might focus on verbs, another on cats. 🐈

Output: A fused super-representation of your input.

4. ⚙️ FeedForward
"Let’s pass this through a brain cell or two."


class FeedForward(nn.Module):
    ...
Each token gets its own mini-MLP (multi-layer perceptron). Basically a tiny 2-layer neural network that says, “Let me make sense of this attention mess.”

5. 🧱 TransformerEncoderBlock
"Attention + brain cells + normalization = genius."


class TransformerEncoderBlock(nn.Module):
    ...
This stacks:

Multi-head self-attention

Add & LayerNorm (residuals make deep networks happy)

Feedforward + more Norm

One block = one layer of the encoder. Stack N of them, your model starts understanding stuff.

6. 🔁 TransformerEncoder
"6 brainy layers of attention and feedforward."


class TransformerEncoder(nn.Module):
    ...
Wraps the embedding, positional encoding, and multiple encoder blocks into one glorious brain tower 🏰.

7. 🔥 TransformerDecoderBlock
"Self-attention... but blindfolded."


class TransformerDecoderBlock(nn.Module):
    ...
Masked self-attention: A word can only look at past words — no peeking ahead! 👀❌

Cross-attention: Looks at the encoder’s output for help (like cheating off the input sentence)

Feedforward + LayerNorm: As usual

8. 🔄 TransformerDecoder
"Now I can speak."


class TransformerDecoder(nn.Module):
    ...
Just like the encoder but:

Learns to generate outputs token by token

Uses causal masks

Outputs logits (not softmaxed)

9. 🌐 Transformer
"The full model, end-to-end."


class Transformer(nn.Module):
    ...
Encoder: Understands the input

Decoder: Generates the output

Output: Token logits → ready for softmax & sampling

🔒 generate_subsequent_mask()
"No peeking ahead!"


def generate_subsequent_mask(seq_len):
    return torch.tril(torch.ones((seq_len, seq_len)))
This creates a lower-triangular matrix that blocks future tokens. Think of it like blinders for autoregressive generation.

🧪 Test Run
At the bottom of the file:


if __name__ == "__main__":
    ...
This runs a fake batch of data (random tokens) through the full model to verify dimensions.


$ python transformer_from_scratch.py
Transformer output shape: torch.Size([2, 10, 10000])
If you see that — 🏆 congrats, your Transformer is alive.

🧪 What's Next?
You can now:

🧠 Train it on toy tasks (copying, reversing)

🐒 Build GPT by deleting the encoder (decoder-only)

🖼️ Use it for image patches (ViT)

🤯 Or just tell your friends you coded a Transformer from scratch — because you did.

🙌 Credit
Built by [YOU], with help from ChatGPT — your friendly AI architect.
Inspired by the legendary paper: “Attention is All You Need” (2017)

📜 License
MIT. Copy it, hack it, train it, transform it.
