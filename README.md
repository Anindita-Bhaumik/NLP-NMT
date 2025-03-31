# NLP-NMT
Neural Machine Translation (NMT) system that could automatically translate sentences written in English to an Indian Language (Bengali and Hindi).The NMT is encoder-decoder architecture, consisting 2 components: Encoder and Decoder with Attention and Beam Search. 
The model architecture that is used in NMT is encoder-decoder architecture, which consists of two components: an Encoder and a Decoder with Attention and Beam Search. The encoder, which is based on BiGRU Neural model, takes the source language sentence (English) as input and learns a representation for it; this representation is then fed to the decoder, a GRU model, that then decodes the target language sentence (Bengali and Hindi) word by word.
The model uses a Bidirectional GRU (BiGRU) encoder, an attention mechanism, and a GRU-based decoder.
Model Components:
(a) Encoder (BiGRU):
•	Inputs: A sequence of word indices (source sentence).
•	Embedding layer: Converts word indices into dense vector representations.
•	Bidirectional GRU: Processes the sentence in both forward and backward directions, concatenating hidden states.
•	Final hidden state: A linear layer transforms the concatenated hidden state to the correct shape before passing it to the decoder.
(b) Attention Mechanism:
•	Computes alignment scores between the decoder hidden state and encoder outputs.
•	Uses a feedforward network to learn attention scores.
•	Applies SoftMax function to get attention weights.
•	These weights determine how much focus each encoder output should get when generating the next word.
(c) Decoder (GRU + Attention):
•	Inputs: Previous word, decoder hidden state, and encoder outputs.
•	Uses an attention mechanism to get a context vector.
•	GRU processes the combined input (embedded word + context vector).
•	A fully connected layer predicts the next word.
•	During training, teacher forcing is used (feeding the actual previous target word as input).
•	Uses beam search.
The inspiration for model architecture is from below:
 
4.	Model objective (loss) functions: 
The loss function used in the model is Cross Entropy Loss (nn.CrossEntropyLoss) from torch library.
criterion = nn.CrossEntropyLoss(ignore_index=0)
This loss expects logits (raw scores before softmax function) as input. The model ignores padding tokens (<PAD> token index = 0) during loss computation. 
This ensures the model does not learn from padded tokens, which do not have semantic meaning.
In the final model, while training, the loss reaches a minimum at around 17th /18th epoch and starts increasing afterwards with the parameters mentioned in point#3 above.
