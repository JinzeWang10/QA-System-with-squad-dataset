# QA System Built on SQuAD Dataset

There are many deep learning models developed for QA systems, but they all require lots of resources to train and fine-tune. Here I choose an unsupervised learning method - cosine distance to solve this problem. The whole process can be divided to two parts:

<ol>
<li> Find the exact sentence in the context where the answer should come from.
<li> Extract the answer from that sentence.
</ol>

### Get Sentences and Sentence Embedding

First I used Textblob to do the intelligent sentence splitting job. It is doing pretty well. And here I use sentence embedding instead of word or phrase embedding since it takes care of the order of words in a sentence, which is very important in this problem. I used SBert for sentence embedding details can be found here: https://www.sbert.net/docs/pretrained_models.html#multi-qa-models

### Find the Sentence where answers come from

Now we have created a embedding for each sentences and questions. We want to compute the similarity between them, so I compute the cosine distance between them and find the sentence with the highest similaity to the questions. I can also use Euclidean distance, but euclidean distance does not care for alignment or angle between the vectors whereas cosine takes care of that. Direction is important in case of vectorial representations.

### Model Performance

The prediction accuracy is 67% using cosine distance.

### Further Works

I still can't find a method to efficiently extract answer from the sentence. I tried the dependency parsing and match the root of question and the sentence, it works well in some cases. But some questions will be asked in a different way. For example, we have sentence "she start her career in 1985 and she rose to fame in 1999" and question "When did she start to be popular?". If we use root match, we will easily match word "start", which will leads to a wrong answer.

So for now, I think we still need to use Deep Learning method to match them to get a good result. I will build a QANet model in the future if I had time.
