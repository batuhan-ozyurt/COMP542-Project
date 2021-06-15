# COMP542-Project

InferSent: I want to implement this as a first baseline. It generates sentence embeddings using GloVe pretrained embeddings and a BiLSTM. At each time step, take the concatenation of two LSTM hidden vectors and do max pooling on the vectors to get the sentence embeddings. For a single sentence task, use a 512D MLP classifier, for sentence-pair tasks, input u;v;|u-v|;|u*v| to the 512D MLP classifier.

You can augment the InferSent Model with pretrained ELMo and CoVe.

ELMo can be integrated into almost all neural NLP tasks with simple concatenation to the embedding layer. 

CoVe model is just a BiLSTM, which is the encoder of a seq2seq model trained on a machine translation task. You feed pretrained GloVe vectors into this BiLSTM to get CoVe embeddings, and then you concatenate CoVe and GloVe embeddings to get the final embedding.
Two issues with CoVe: 
1- Supervised pretraining is required.
2- Task specific model is required.
ELMo is better than CoVe because its pretraining is unsupervised.
Both ELMo and CoVe require task specific architectures. This issue is resolved with BERT and GPT like models.

Question: How do we integrate CoVe into our InferSent model? 
Possible Answer: Concatenate GloVe, ELMo and CoVe all together in the embedding layer.
