# Context-sensitive-Spelling-Correction
The goal of the project is to implement context-sensitive spelling correction. The input of the code will be a set of text lines and the output will be the same lines with spelling mistakes fixed.


## My proposed solution to this problems

First of all, the dataset which Norvig's solution was trained on is small and it doesn't contain variaty of words, so in my solution the corpus of words that I used is from the ngram data file which contain large amount of words in different shapes. This limits the number of the unknown words that the model faces.

Secondly, his error model was prioritizing the candidates with small edit distance. However, that is not always the case as. So to make the model more flexable, I allowed the candidates to be a list of all 1 and 2 edits words plus the original word. This solution rely on the fact that the model will make the right decision and choose the suitable word for the given context.

Finally, his solution can not look at the context of the word which increase the probability of making errors while choosing from the candidates. To solve this problem, I used bigram model to look at the context of the word and propose the correction with the highest conditional probability, highest frequenct, and lowest edit distance score in a weighted manner.

### Why did I choose bigram model?

- Bigram models are faster and require less memory than 5-gram models because they consider pairs of adjacent words rather than groups of five words at a time.
- In a bigram model, the probability of a word depends only on the preceding word, so it can handle unseen words better than a 5-gram model, which would require seeing the preceding four words to make a prediction.
- Simplicity and ease of implementation

### Why did I choose these specific weights for the scores of the candidates?

- my_solution.conditional_probs_weight = 0.9352175845886633
- my_solution.frequency_weight = 0.03328620660509829
- my_solution.edit_distance_weight = 0.8554663627569048

Using trial and error on the training dataset, I came to a conclusion that these are the most suitable weights to use.

I assigned these values randomly for 50 trials and took the best preforming weights on the training set and then reported their results on the validation set
