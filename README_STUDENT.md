Key Concepts to Understand
Cosine Similarity
- Measures angle between vectors
- Range: -1 to 1 (we exponentiate to get positive values)
- Doesn't depend on magnitude, only direction

Word Embeddings (GloVe)
- Each word → fixed-length vector
- Similar words → similar vectors
- Averaging loses word order!

Sentence Embeddings (Transformers)
- Whole sentence → single vector
- Captures context and word order
- Better for semantic similarity
 
OpenAI Embeddings
- State-of-the-art quality
- Large models = better performance
- Costs money (but has free tier)

Quick Start (3 steps)
1. **Install dependencies:**
   ```bash
   pip install streamlit numpy sentence-transformers openai gdown matplotlib pandas
   ```
2. **Set OpenAI API Key:**
   ```bash
   export OPENAI_API_KEY="your-key-here"
   ```
3. **Run the app:**
   ```bash
   streamlit run YOUR_FILE_NAME.py
   ```

# What You Need to Implement
All three tasks are marked with `# TODO` comments in the code:

Task I: `cosine_similarity(x, y)`
Task II: `averaged_glove_embeddings_gdrive()`
Task III: `get_sorted_cosine_similarity()`


How to Test
 Test 1: Basic (Make sure it runs)
- Categories: `Flowers Colors Cars Weather Food`
- Input: `"Roses are red, trucks are blue"`
- Check: All models produce results
- Observation: All models successfully processed the request and generated probability distributions, confirming the pipeline is functional.

Test 2: Sentiment
- Categories: `Positive Negative`
- Input 1: `"The movie was upsetting"`
- Input 2: `"This is terrible"`
- Check: Correct sentiment detection
- observation: 
    1. GloVe: Classified as Positive (Incorrect).

    2. Sentence Transformer: Classified as Negative at 63.7% (Correct).

    3. OpenAI: Classified as Negative (Small: 90%, Large: 86.2%) (Correct).

-Analysis: GloVe fails here because it uses a simple average of word vectors. Since "movie" and "the" are neutral and it cannot grasp the emotional weight of "upsetting" in a specific syntactic context, it fails to capture the negative sentiment.

# What to Include in Analysis

# Part A:
Answer these questions:
1. Which models got it right? 
The Transformer-based models (OpenAI and Sentence Transformer) showed sensitivity to the distinction, whereas GloVe failed to differentiate the two.

Why did some fail?
2. Why did some fail? 
GloVe failed because it is a Bag-of-Words model. It calculates the sentence embedding by averaging the vectors of individual words. Mathematically, $Vector(\text{Milk}) + Vector(\text{Chocolate})$ is identical to $Vector(\text{Chocolate}) + Vector(\text{Milk})$. It has no mechanism to understand that the last word in these phrases usually acts as the "head" (the actual object).

3. What does this reveal about word order?
It reveals that syntax determines semantics. Static embeddings (GloVe) lack "Positional Encoding," making them "blind" to structure. Modern Transformers use attention mechanisms to weigh words based on their position, allowing them to understand that "Milk Chocolate" is a type of chocolate (Snack), while "Chocolate Milk" is a type of milk (Beverage).


# Part B: Model Comparison
Compare across:
- Accuracy on test cases
- Dimensionality vs performance
- Speed/response time
- Word order sensitivity

| Feature | GloVe | Sentence Transformer | OpenAI (Small/Large) |
| :--- | :--- | :--- | :--- |
| **Accuracy** | Low (Fails on sentiment/order) | High (Good context grasp) | Highest (Superior nuances) |
| **Speed/Latency** | Instant (Local calculation) | Moderate (Local GPU/CPU) | High Latency (API/Network) |
| **Word Order** | Insensitive (Averaging) | Sensitive (Attention-based) | Highly Sensitive |
| **Best Use Case** | Simple keyword matching | Real-time local apps | Complex reasoning/Nuance |


# Part C: Real-World Applications
Part C: Real-World Applications
-Pick 3 groups of everyday categories (e.g., Kitchen, Furniture, Baby, Outdoor).
-For each group, write 2 sentences using similar words but different word order.

Group 1: Apple (Technology vs. Fruit)
Input A: "Apple Watch" → Technology

Input B: "Watch Apple" → Fruit

Observation: Transformers successfully identified that "Watch" as a noun (A) implies a gadget, while "Watch" as a verb (B) implies observing the fruit.

Group 2: Glass (Container vs. Material)
Input A: "Water Glass" → Container (All models correct)

Input B: "Glass Water" → Material (Only OpenAI Large identified as Material)

Observation: Most models struggle with "Glass Water" due to the strong association between these words and containers. OpenAI Large’s higher dimensionality allows it to detect the subtle shift where "Glass" modifies "Water" as a material property.

Group 3: Paper (Action vs. Office)
Input A: "Paper Shredder" → Office (All models correct)

Input B: "Shred Paper" → Action (GloVe: Action; Others: Office)

Observation: Interestingly, GloVe got this "right" because it placed heavy vector weight on the verb "Shred." The Transformer models were slightly biased by the strong global association between "Paper" and "Office," showing that even advanced models can sometimes prioritize keyword association over grammatical intent in short phrases.

Example:
-baby furniture safety covers → Category: Furniture
-furniture for baby room → Category: Baby / Furniture
-Observe how word position changes meaning and category assignment.
-Briefly explain why the category changes for each pair.

 Bonus: Deployment Checklist
- [Done] Push code to GitHub
- [Done] Sign up for Streamlit Cloud
- [Done] Connect GitHub repo
- [Done] Add OPENAI_API_KEY to Secrets
- [Done] Deploy!
- [Done] Test the live URL
- [Done] Submit URL in deployment.txt


Submission Checklist
Before you submit:
-  All three tasks completed and working
- Tested with at least 5 different inputs
- Analysis document (2-3 pages) written
- Comparison tables included
- Screenshots taken
- Code is commented
- README read completely
- (Bonus) App deployed and URL tested

Helpful Links
- **Streamlit Docs:** https://docs.streamlit.io
- **OpenAI API:** https://platform.openai.com
- **Sentence Transformers:** https://sbert.net
- **NumPy Docs:** https://numpy.org/doc
*Remember: The goal is to learn, not just to complete. Take your time and understand each concept.*