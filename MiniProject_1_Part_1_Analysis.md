# Mini Project 1 Part 1 Analysis
Author: Xindi Xu

## Part A:  
Answer these questions:  
1. Which models got it right?  
	- Sentence Transformer and OpenAI models achieved higher accuracy, while GloVe had the lowest.
2. Why did some fail?  
	- GloVe fails because the code averages word embeddings and ignores word order. Even increasing the embedding dimensionality does not fully solve this issue (see **Table 1** in Appendix).
3. What does this reveal about word order?  
	  - Word order is important for sentence meaning. Changing the order can alter the meaning of a sentence, so models that are sensitive to word order perform better than those that are not.
## Part B: Model Comparison  
Compare across:  
- Accuracy on test cases
- Dimensionality vs performance
- Speed/response time
- Word order sensitivity

**Summary:**

| Model                | Accuracy | Dimensionality vs performance                                    | Speed    | Word order sensitivity |
| -------------------- | -------- | ---------------------------------------------------------------- | -------- | ---------------------- |
| GloVe                | lowest   | Increasing dimensions from 25d to 100d gives limited improvement | fast     | non-sensitive          |
| Sentence Transformer | medium   | /                                                                | moderate | sensitive              |
| OpenAI               | highest  | small vs large models show similar performance                   | slow     | sensitive              |

**Explanation for Dimensionality vs performance:**
- **GloVe:** Even when increasing the embedding dimensionality from 25d to 100d, performance improves only slightly. Specifically, the top predicted category often remains incorrect, although the confidence score tends to decrease (see **Table 1** and **Table 2** in Appendix; the confidence score decrease by 0.1-0.2).
- **OpenAI small vs large:** The performance difference between the small and large models is minimal. And sometimes the small model predicts correctly while the large model predicts incorrectly (see **Table 1** in Appendix; OpenAI_large_3072 predicted the wrong category: "Flowers").
# Part C: Real-World Applications  
Part C: Real-World Applications  
- Pick 3 groups of everyday categories (e.g., Kitchen, Furniture, Baby, Outdoor).  
- For each group, write 2 sentences using similar words but different word order.  
  
Example:  
- baby furniture safety covers → Category: Furniture  
- furniture for baby room → Category: Baby / Furniture  
- Observe how word position changes meaning and category assignment. 
- Briefly explain why the category changes for each pair.

**Observation:**
- Changing the position of the key noun can change the meaning and category assignment. For example, (see **Table 3** and **Table 4** in the Appendix), from Sentence 1 to Sentence 2, the predictions of the Sentence Transformer and OpenAI models changed.

**Explanation:**
- When a key noun is moved or modified, models that are sensitive to word order adjust the predicted category accordingly. In contrast, models that simply average word embeddings are less sensitive, so word order has less influence on their predictions. 

## Appendix
Some of the experimental results are included in the Appendix.
### 1. Basic Test

- Input:
	- Categories: Flowers Colors Cars Weather Food
	- Sentence: Roses are red, trucks are blue, and Seattle is grey right now
- Result: see Table 1

Table 1:

| Model                    | Top Category | Confidence Score |
| ------------------------ | ------------ | ---------------- |
| glove_25d                | Food         | 2.2445           |
| glove_50d                | Food         | 2.0993           |
| glove_100d               | Food         | 1.9550           |
| sentence_transformer_384 | Colors       | 1.7090           |
| openai_small_1536        | Colors       | 1.3675           |
| openai_large_3072        | Flowers      | 1.3515           |

### 2. Sentiment Test
- Input:
	- Categories: Positive Negative
	- Sentence: The movie was upsetting
- Result: see Table 2

Table 2:

| Model                    | Top Category | Confidence Score |
| ------------------------ | ------------ | ---------------- |
| glove_25d                | Positive     | 1.9910           |
| glove_50d                | Positive     | 1.8110           |
| glove_100d               | Positive     | 1.6073           |
| sentence_transformer_384 | Negative     | 1.1408           |
| openai_small_1536        | Negative     | 1.2862           |
| openai_large_3072        | Negative     | 1.2693           |
### 3. Real-World Applications

Categories: Furniture Baby Kitchen

#### Baby Group：
- Sentence 1: baby safety covers in room
- Result: see Table 3
- Sentence 2: safety covers for baby room
- Result: see Table 4
Table 3:

| Model                    | Top Category | Confidence Score |
| ------------------------ | ------------ | ---------------- |
| glove_25d                | Baby         | 2.3181           |
| glove_50d                | Baby         | 2.1951           |
| glove_100d               | Baby         | 2.1461           |
| sentence_transformer_384 | Baby         | 1.2683           |
| openai_small_1536        | Furniture    | 1.3709           |
| openai_large_3072        | Furniture    | 1.3351           |
Table 4:

| Model                    | Top Category | Confidence Score |
| ------------------------ | ------------ | ---------------- |
| glove_25d                | Baby         | 2.3495           |
| glove_50d                | Baby         | 2.2485           |
| glove_100d               | Baby         | 2.1806           |
| sentence_transformer_384 | Furniture    | 1.2459           |
| openai_small_1536        | Baby         | 1.4034           |
| openai_large_3072        | Baby         | 1.2990           |
