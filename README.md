# Next Word Prediction (NLP)

## Project Overview

This project implements a **Next Word Prediction** system using classic **NLP** techniques, specifically **n-gram models**. The goal is to predict the next word given a sequence of preceding words, much like a simplified version of an autocomplete feature.

**Key Objectives:**
- Understand the basics of language modeling.
- Experiment with **bigram** and **trigram** models.
- Explore **smoothing** techniques (Add-One / Laplace).
- Evaluate model performance using train/test splits.

This project was completed as part of my learning journey in **Artificial Intelligence / Machine Learning** and serves as a demonstration of foundational NLP concepts.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset and Preprocessing](#dataset-and-preprocessing)
3. [Modeling Approach](#modeling-approach)
4. [Evaluation](#evaluation)
5. [Results](#results)
6. [How to Run](#how-to-run)
7. [Project Structure](#project-structure)
8. [Future Improvements](#future-improvements)
9. [License](#license)

---

## Dataset and Preprocessing

**Four public-domain books** were combined from [Project Gutenberg](https://www.gutenberg.org/):

1. *The Adventures of Sherlock Holmes* by Arthur Conan Doyle  
2. *Moby Dick* by Herman Melville  
3. *Pride and Prejudice* by Jane Austen  
4. *Alice's Adventures in Wonderland* by Lewis Carroll

### Data Cleaning Steps

1. **Lowercasing**  
2. **Removing punctuation** (except apostrophes for contractions)  
3. **Whitespace normalization**  
4. **Tokenization**

The cleaned tokens are saved to `data/combined_tokens.json` for quick access.

---

## Modeling Approach

1. **Bigram Model**  
   - Each word is predicted using only the immediately preceding word.

2. **Trigram Model**  
   - Each word is predicted using the two preceding words for more context.

3. **Smoothing**  
   - Implemented **Add-One (Laplace)** smoothing for the bigram model to handle unseen `(word1 -> word2)` pairs.

### Code Highlights

- **`build_bigram_model` / `build_trigram_model`**: Build raw frequency-based models.  
- **`predict_next_word_bigram` / `predict_next_word_trigram`**: Predict next word using maximum likelihood estimation.  
- **`build_bigram_model_addone` / `predict_next_word_bigram_addone`**: Add-One smoothing approach for bigram.  
- **Interactive Cells**: Users can type a word or two to see the model’s predicted next word in real time.

---

## Evaluation

The tokens were splitted into **80% training** and **20% testing**. **Exact next-word accuracy** were measured:

- **Bigram Accuracy**: Checks if the most likely next word matches the actual next word in the test set.  
- **Trigram Accuracy**: Similar but uses pairs of words as context.

*(Note: Exact next-word matching is a strict metric, especially for literary texts, so the model’s accuracy may appear lower than expected due to the diverse vocabulary and writing styles.)*

---

## Results

| Model                 | Accuracy (Test Set)  |
|-----------------------|----------------------|
| **Bigram**            | ~ 0.10 - 0.15 (example) |
| **Trigram**           | ~ 0.12 - 0.18 (example) |
| **Add-One Bigram**    | ~ 0.10 - 0.15 (similar or slightly higher) |

**Key Observations:**
- Accuracy is modest, which is typical for basic n-gram models on diverse literary text.
- Adding 4 books instead of 1 did not dramatically boost accuracy due to style differences and the limited size of the data.
- Simple smoothing (Add-One) showed only minor improvements.

**Inferences and Explanations:**
- **N-gram Limitations:** Classic n-gram models capture only local context (one or two preceding words) and lack advanced smoothing (e.g., Kneser–Ney), which can lead to modest accuracy in diverse text.
- **Literary Text Complexity:** Since our data comes from multiple literary sources with varying styles and vocabularies, exact next-word prediction becomes even more challenging.
- **Modern Techniques:** By leveraging modern language models or deep learning approaches (e.g., RNNs, Transformers), significantly higher accuracies can be achieved, although these methods demand larger datasets and more complex computational frameworks.


---

## How to Run

1. **Clone the Repository**  
   ```bash
   git clone https://github.com/berkinksk/Next-Word-Prediction-NLP.git
   cd Next-Word-Prediction-NLP
   ```

2. **Install Dependencies**  
   Make sure you have Python 3.7+ and run:
   ```bash
   pip install -r requirements.txt
   ```
   (If you haven’t created a requirements.txt, you can list packages like matplotlib, etc.)

3. **Open Jupyter Notebook** 
   ```bash
   jupyter notebook
   ```
- Navigate to notebooks/Data_Preprocessing.ipynb.
- Run each cell in order to build and evaluate the models.

---

## Project Structure

   ```bash
   Next-Word-Prediction-NLP/
├── data/
│   ├── sherlock_holmes.txt
│   ├── moby_dick.txt
│   ├── pride_and_prejudice.txt
│   ├── alice_in_wonderland.txt
│   └── combined_tokens.json
├── notebooks/
│   └── Data_Preprocessing.ipynb
├── .gitignore
├── LICENSE
└── README.md
   ```

## Future Improvements

1. **Advanced Smoothing**
- Kneser–Ney or Good–Turing can be implemented to handle unseen contexts more effectively.

2. **Backoff / Interpolation**
- trigram → bigram → unigram probabilities can be combined.

3. **Neural Language Models**
- Using RNNs (LSTM/GRU) or Transformers can be considered for significantly better performance.

4. **Perplexity**
- Model quality can be evaluated with perplexity, a common NLP metric.

5. **Larger or More Homogeneous Dataset**
- Training on a more focused or much larger dataset may yield higher accuracy.

---

## License

This project is licensed under the **MIT** License. You may use, modify, and distribute this software as long as the license terms are observed.