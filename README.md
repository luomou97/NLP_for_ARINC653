# NLP_for_ARINC653
using NLP-based technologies to parse ARINC 653 requirements, extract its knowledge, construct Ontology and execute formalization.

# Abstract
Accuracy and rigour are vital indicators of the software requirement specification (SRS), especially for the OS requirement specification. A high-quality SRS should clearly depict the system behaviors yet leave no fatal vulnerability. Formal verification could definitely help achieve this goal, but it requires domain expertise and intensive manual analysis for building formal model, such as an ontology. However, as knowledge about entities and their relations in the ontology is scattered over the content in heterogeneous formats (plain text, pseudocode, XML, etc.) for many OS SRS documents, it is laborious and error-prone to manually integrate the knowledge from various formats. Recently, fast-growing natural language process (NLP) techniques do well in harvesting knowledge extraction for the downstream tasks. To this end, we propose a novel and practical NLP-based approach to automatically analyze and extract knowledge from the OS SRS. Technically, we combine the NLP techniques with domain-specific naming and lexical rules for entity recognition for building ontology and then apply information extraction and relation formalization for relation extraction (in terms of guards). We evaluate our approach on the industrial aviation ARINC653 OS standard, and assess the quality of our generated ontology against that induced by the domain expert. We further apply this approach to the historical ARINC653 standards and evaluate the performance. Results show that our approach indeed helps in knowledge integration and aid for specification formalization.

#### For the details of our approach, please refer to the below supplemental materials:
- [Inconsistencies](https://github.com/luomou97/NLP_for_ARINC653/tree/main/Inconsistencies) 
- [Relation Extraction](https://github.com/luomou97/NLP_for_ARINC653/tree/main/Relation%20Extraction) 
- [Relation Formalization](https://github.com/luomou97/NLP_for_ARINC653/tree/main/Relation%20Formalization) 
- [Ontology](https://github.com/luomou97/NLP_for_ARINC653/tree/main/Ontology) 
- [Typos](https://github.com/luomou97/NLP_for_ARINC653/tree/main/Typos)
