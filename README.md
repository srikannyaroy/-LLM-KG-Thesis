# -LLM-KG-Thesis
An AI-based system that combines Large Language Models (LLMs) with Knowledge Graphs to improve structured information retrieval and reduce hallucinations. The project integrates RAG (Retrieval-Augmented Generation),  and graph-based reasoning for accurate and explainable outputs.
#  LLM-Based Knowledge Graph Construction from Unstructured Documents

## Overview
This project builds an **interactive knowledge graph** from unstructured documents (PDFs/text) using a **Large Language Model (Mistral-7B)**.

The system extracts **semantic relationships** using an LLM and enhances them with **contextual proximity (co-occurrence analysis)** to generate a rich, structured graph.  
The final output is an **interactive visualization** using PyVis.

---

## 🚀 Key Features

-  Load unstructured documents (PDF/TXT)
-  Smart text chunking with overlap
-  LLM-based triple extraction (node₁, edge, node₂)
-  Contextual proximity for implicit relationships
-  Graph construction using NetworkX
-  Community detection (Girvan–Newman algorithm)
-  Interactive visualization using PyVis
-  CSV caching for scalability and recovery

---

## 🏗️ Project Pipeline
Documents → Chunking → LLM Extraction → JSON Parsing → Graph Edges
→ Contextual Proximity → Merge Edges → NetworkX Graph
→ Community Detection → PyVis Visualization


---

## ⚙️ Technologies Used

- LLM: Mistral-7B (via Ollama)
- Framework: LangChain
- Graph Processing: NetworkX
- Visualization: PyVis
- Data Handling: Pandas, NumPy

---

## 📂 Project Structure

├── DEMO1.ipynb  
├── extract_graph.ipynb  
├── helpers/  
│   ├── df_helpers.py  
│   ├── prompts.py  
├── data_input/  
├── data_output/  
├── docs/  
│   └── index.html  

 Core Components

1. Text Chunking
Uses `RecursiveCharacterTextSplitter`:
- chunk_size = 500
- chunk_overlap = 50

Ensures context preservation and LLM compatibility.

2. LLM-Based Extraction (df2Graph)
- Each chunk is processed by Mistral-7B
- Extracts triples in JSON format:

{
  "node_1": "Diabetes",
  "edge": "treated_by",
  "node_2": "Metformin"
}

- Converts unstructured text into structured relationships

3. Contextual Proximity
- Adds edges based on co-occurrence of concepts in the same chunk
- Captures implicit relationships missed by the LLM
- Uses frequency (count) as edge strength

 4. Edge Merging
- Combines:
  - LLM semantic edges
  - Contextual proximity edges
- Aggregates weights for stronger relationships
  
 5. Graph Construction
- Built using NetworkX
- Nodes represent concepts
- Edges represent relationships
- Weight represents strength of relation

 6. Community Detection
- Uses Girvan–Newman algorithm
- Detects clusters of related concepts
- Each cluster assigned a unique color

7. Visualization
- PyVis generates an interactive HTML graph
- Node size = degree
- Edge thickness = weight
- Colors = communities


---

## 📊 Output

- graph.csv → extracted relationships
- chunks.csv → processed text chunks
- docs/index.html → interactive graph

---

Important Design Decisions

- No embedding model used
- No vector database used
- Focused on structured knowledge graph construction
- Hybrid approach: LLM + statistical co-occurrence
---

## 📈 Insights from Graph

- Identifies central concepts (high-degree nodes)
- Reveals hidden relationships
- Separates thematic clusters
- Enables knowledge exploration

## ⚡ How to Run

1. Install dependencies
pip install -r requirements.txt

2. Start Ollama
ollama run mistral

3. Run notebooks
- DEMO1.ipynb (small data)
- extract_graph.ipynb (full data)

4. Open output
docs/index.html
