# Biomedical Knowledge Graph Primer

This project demonstrates how to build and query a **small biomedical knowledge graph** using real public biological data sources. The entire workflow is implemented in a single Jupyter notebook that retrieves data, constructs an RDF graph, performs SPARQL queries, and enables natural-language interaction with the graph using an LLM.

The goal is to provide a **clear, practical example** of how biomedical knowledge graphs can be constructed and explored using modern Python tools.

---

## Overview

The notebook performs the following steps:

1. Retrieve pathway participants from **Reactome**
2. Extract proteins involved in the **RAF/MAP kinase signaling pathway**
3. Query **ChEMBL** for drug–target relationships
4. Query the **Open Targets Platform GraphQL API** for gene–disease associations
5. Construct an **RDF knowledge graph** (Turtle format)
6. Query the graph using **SPARQL**
7. Enable **natural language queries** using an LLM

The resulting graph connects four biological entity types:

Drug → Protein → Disease  
          ↓  
        Pathway

---

## Data Sources

This project integrates several public biological resources:

- **Reactome** — pathway and molecular interaction data  
- **ChEMBL** — drug–target relationships  
- **Open Targets Platform** — gene–disease associations  

All data is retrieved programmatically using public APIs.

---

## Repository Structure

```
talk-to-your-knowledge-graph-primer
├── README.md
├── data_processed
├── data_raw
├── notebooks
│   └── talk_to_your_graph_python_notebook.ipynb
├── pyproject.toml
├── requirements.txt
└── uv.lock
```

The notebook contains the complete workflow including:

- data retrieval
- graph construction
- visualization
- SPARQL queries
- natural language querying

---

## Environment Setup

This project uses **uv** for Python environment management.

Create the virtual environment:

```
uv venv
```

Install dependencies:

```
uv pip install -r requirements.txt
```

Launch the notebook environment:

```
uv run jupyter lab
```

Then open:

```
notebooks/talk_to_your_graph_python_notebook.ipynb
```

---

## Knowledge Graph Construction

The notebook integrates data from the three biological sources and constructs an RDF graph stored as:

```
data_processed/graph.ttl
```

The graph contains the following entities:

- A biological pathway
- Proteins
- Drugs
- Diseases

Relationships include:

- `Drug → targets → Protein`
- `Protein → associatedWith → Disease`
- `Protein → participatesIn → Pathway`

---

## Querying the Graph

### SPARQL Queries

The graph can be queried directly using **SPARQL** through RDFLib.

Example query:

```sparql
SELECT ?drugLabel
WHERE {
  ?drug ex:targets ?protein ;
        rdfs:label ?drugLabel .
  ?protein rdfs:label|skos:altLabel "EGFR" .
}
```

---

### Natural Language Queries (this requires an (e.g. OpenAI) LLM API key)

The notebook also demonstrates a **"talk to your graph"** workflow:

1. A user asks a question in natural language
2. An LLM converts the question into SPARQL
3. The SPARQL query is executed against the graph
4. The results are summarized in natural language

Example questions:

```
Which drugs target EGFR?
Which proteins participate in the RAF/MAP kinase cascade?
Which drugs target proteins associated with melanoma?
```

---

## Purpose

This project is intended as a **learning exercise** demonstrating:

- biomedical data integration
- RDF knowledge graph construction
- graph exploration in Python
- SPARQL querying
- LLM-assisted querying of structured biological data

The notebook provides a compact but realistic example of how knowledge graphs can support biomedical research workflows.

---

## License

This project uses publicly available datasets and is intended for educational purposes.
