# Context-Sensitive Spelling Correction

**Context-sensitive spelling correction model** utilizes n-grams (1-5) to improve the accuracy of spelling correction based on the surrounding text. Unlike traditional approaches, such as Norvig's spell corrector, which relies on unigrams and ignores context, this model enhances correction precision by considering the context of each word in the sentence.

## Features
- **Context-aware correction:** Uses n-grams to analyze word context and improve spelling suggestions.
- **Beam Search:** Efficiently explores candidate corrections, selecting the most probable word based on context.
- **Evaluation with Realistic Data:** Utilizes datasets like the Brown corpus and the `sage` library to simulate real-world misspellings for more accurate testing.

## Example: Why Context is Needed

One of the main reasons for moving away from **Norvig’s spell corrector** is its use of a **unigram-based approach**, which treats each word independently. This approach limits the ability to handle contextual relationships in sentences. Below is a comparison between Norvig’s model and my context-aware model:

| **Original Sentence**                | **Norvig’s Output**           | **Context-Sensitive Corrector Output** |
|--------------------------------------|-------------------------------|---------------------------------------|
| a bad cas of the                     | <span style="color:red;">a bad was of the</span>  | <span style="color:green;">a bad case of the</span>                    |
| He fel in a puddle.                  | <span style="color:red;">he few in a puddles</span> | <span style="color:green;">he fell in a puddle.</span>                  |
| He did not fel well.                 | <span style="color:red;">he did not few well</span>  | <span style="color:green;">he did not feel well.</span>                 |


### Explanation of Errors:
- **"cas" → "was"**: Norvig's model incorrectly corrects "cas" to "was" instead of "case."  
   - **Error**: The correct correction is "case" to maintain the meaning of the sentence.
  
- **"fel" → "few"**: Norvig's model changes "fel" to "few," which is grammatically incorrect in this context.  
   - **Error**: "Fel" should be corrected to "fell" or "feel" depending on the context.

- **"fel well" → "few well"**: Norvig's model turns "fel" to "few," which results in a nonsensical sentence.  
   - **Error**: "Fel" should be corrected to "feel" for a grammatically and semantically correct sentence.

### Context-Sensitive Corrector:
- **"cas" → "case"**: My model correctly identifies that "cas" should be corrected to "case," preserving the meaning of the sentence.
- **"fel" → "fell" or "feel"**: The model takes context into account and suggests "fell" or "feel" as the correct options depending on the surrounding words, improving grammatical and semantic accuracy.

The need for **context-aware spelling correction** is evident here, as **n-grams** (which capture context) allow for more accurate predictions compared to Norvig’s unigram-based approach.

## Results

### **Sentence-Level Evaluation:**

For sentence-level evaluation, I evaluated how well each model can correct sentences with multiple mistakes. The accuracy of corrections was calculated based on token-level matches between the ground truth and the corrected sentences.

- **Accuracy on Sentence-Level:**  
    The **context-sensitive model** **outperformed** Norvig (75.17% accuracy), reaching **97.12% accuracy**, significantly improving sentence-level spelling correction.

## Summary

In summary, **Norvig Corrector** performs better in terms of speed, both at the word and sentence levels. However, **Context-Sensitive Corrector** significantly outperforms **Norvig Corrector** in terms of accuracy, especially at the sentence level. The trade-off between processing speed and accuracy should be considered based on the application requirements.
