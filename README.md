1. What this repository is about

The primary goal behind creating this repository was to understand the internal workings of Retrieval-Augmented Generation (RAG) systems.

Instead of relying on high-level frameworks like LangChain, this project intentionally implements the RAG pipeline in a more explicit and manual manner. The aim is to keep every stage visible and modifiable, so that different design choices (chunking, embedding, retrieval, prompt formulation) could be learned about and tuned independently.

While the project was designed as a learning and experimentation repository rather than an over-engineered or heavily parameterized system.

2. Why the legal text corpus

The legal corpus was selected primarily because the novels i was familiar with were too short and not available to be used publically for things like RAG. Legal corpus offered a very large text corpus ensuring our space isn't sparse while being free to use by anyone

A legal text corpus was chosen primarily for unrestricted use and sharing as  
Most narrative or fictional datasets that the author was familiar with were either too small making sparse spaces or not publicly distributable for use in projects like RAG.

Legal corpora, on the other hand, offered:
A very large volume of text, reducing sparsity in the embedding space along with Strong semantic structure (cases, sections, precedents, statutes) in case of judgements and best of all, Public availability. 

This made legal text a good candidate for testing how well semantic retrieval behaves at scale, especially in a domain where precision and grounding matter.

3. What is the scope/ what to expect 

The main aim behind this is to Make a retrieval system which is able to retrieve relevant chunks of text related to query of user. And to see how much can it be optimized further using rewriting of prompt for retrieval, the challanges faced with building systems like this and other valuable experiences and insights.

The main objective of this project is to build a retrieval system capable of fetching relevant text chunks in response to a user query.
Specifically, 
Chunking and embedding long legal documents
Semantic retrieval using vector similarity
Studying how well retrieved chunks support downstream answers
Exploring challenges such as irrelevant retrievals, weak matches, irrelevant query, query rewriting, when to actually use RAG among others

Bear in mind, this does not aim to provide -
A legal advice system or production-ready application
A benchmarked or optimized commercial solution

4. About Dataset

Three differnt datasets were used to make this particular project -
   1. https://www.kaggle.com/datasets/adarshsingh0903/legal-dataset-sc-judgments-india-19502024 The Supereme Courts' Judgements till 2024. These have pdf of judgements made by Supereme Court of India over the year with each judgement being its own pdf. all the folders and files were parsed and converted to text, which was single most time consuming part of this project. 

   2. https://www.kaggle.com/datasets/nandr39/bharatiya-nyaya-sanhita-dataset-bns The BNS - Bharatiya Nyaya Sanhita Dataset which provided the laws as written with Chapter, Sections etc, as may be required for the query. The smallest of the three datasets however being small and all chapters being completely indipendent, It was included to see how well will small corpus behave if treated otherwise.

   3. https://huggingface.co/datasets/opennyaiorg/InJudgements_dataset Just like the Supereme Courts' Judements, this dataset provides further corpus of judgement from supereme and high courts both. However since a bigger Supereme Courts' Dataset was used, only high courts' judgements were actually used from this dataset in this notebook.

5. Repository Structure
judgment-rag-india/
│
├── notebooks/
│   ├── BeforeFaiss.ipynb     # Data loading, cleaning, and preprocessing
│   ├── AfterFaiss.ipynb      # Embedding generation and FAISS-based retrieval
│
├── RAG_HEARINGS.ipynb     # Not relevant, kept for old reference
├── README.md
├── requirements.txt

6. What this project demonstrates

The experience of working on this helped with 
Understanding of RAG pipelines without framework abstraction
Practical experience with vector embeddings and FAISS
Working with large, real-world text corpora
Awareness of failure and challanges in semantic retrieval systems

7. Future Directions

Applying RAG on selected queries only, not all, hence preventing unnecessary computations
Using more datasets to include richer range of cases - for example finance related cases or household related queries
Better exploring the models' training to realize correct structure or wordings for prompts

8. Cleaned data and Built Faiss Index - 

Preprocessed text chunks and embedding files are not included  in this repository due to size constraints of github.

Access them here - https://drive.google.com/drive/folders/1n36ukuR0DOq_PzO5Roo3BADeF1XdSU5r

The files include:
- chunk_text.pkl
- apex_embed.npy
- bns_embed.npy
- high_embed.npy
