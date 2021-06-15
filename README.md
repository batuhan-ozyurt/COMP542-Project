# COMP542-Project

[Research Log](https://docs.google.com/document/d/1TU-SytN72VAUvIoxig2BsL9KrK_iTZogxV5SyCIbNI4/edit?usp=sharing)

## GLUE Dataset

GLUE is a widely used benchmark for Natural Language Understanding (NLU) tasks. It has nine different tasks that draw attention to various aspects of NLU. These tasks are:

**Single sentence tasks:**

**CoLA:** Binary classification task, each sentence is annotated if it is a grammatical English sentence or not.

**SST-2:** Binar classification task, each sentence is annotated if it has a positive or negative sentiment.

**Two sentence tasks:**

**MRPC:** Given two sentences, the task is to determine if they are semantically equivalent or not.

**QQP:** Given two questions from the Quora website, the task is to determine if they are semantically equivalent or not.

**STS-B:** Given two sentences, the task is to give the pair a similarity score between 1 and 5.

**MNLI:** Given two sentences, a premise and a hypothesis, the task is to predict whether the premise entails the hypothesis (entailment), contradicts the hypothesis (contradiction), or neither (neutral).

**QNLI:** This task converts the SQuAD question answering task into sentence pair classification by forming a pair between each question and each sentence in the corresponding context, and filtering out pairs with low lexical overlap between the question and the context sentence. The task is to determine whether the context sentence contains the answer to the question.

**RTE:** This dataset comes from annual contextual entailment challenges RTE1, RTE2, RTE3 & RTE5.

**WNLI:** In this task, a system must read a sentence with a pronoun and select the referent of that pronoun from a list of choices. To convert the problem into sentence pair classification, we construct sentence pairs by replacing the ambiguous pronoun with each possible referent. The task is to predict if the sentence with the pronoun substituted is entailed by the original sentence

## Baseline 
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

References

Wang, A., Singh, A., Michael, J., Hill, F., Levy, O., &amp; Bowman, S. (2018). GLUE: A Multi-Task Benchmark and Analysis Platform for Natural Language Understanding. Proceedings of the 2018 EMNLP Workshop BlackboxNLP: Analyzing and Interpreting Neural Networks for NLP. https://doi.org/10.18653/v1/w18-5446 

Conneau, A., Kiela, D., Schwenk, H., Barrault, L., &amp; Bordes, A. (2017). Supervised Learning of Universal Sentence Representations from Natural Language Inference Data. Proceedings of the 2017 Conference on Empirical Methods in Natural Language Processing. https://doi.org/10.18653/v1/d17-1070 
