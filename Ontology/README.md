[Ontology_NLP](https://github.com/luomou97/NLP_for_ARINC653/blob/main/Ontology/ARINC653Ontology_ExtractByNLP.owl), please visualize it by [Protégé](https://www.google.com/url?q=https%3A%2F%2Fprotege.stanford.edu%2F&sa=D)

[Ontology_HE](https://github.com/luomou97/NLP_for_ARINC653/blob/main/Ontology/ARINC653Ontology_InducedByProfessor.owl), please visualize it by [Protégé](https://www.google.com/url?q=https%3A%2F%2Fprotege.stanford.edu%2F&sa=D)

green means the Unique for Ontology_NLP; red means the Unique for Ontology_HE. Thus, the real **similarity between Ontology_HE and Ontology_NLP is 86.27%**. More importantly, **our NLP-based technique is able to dig out 4 unique entities that human experts missed.**
![image](https://github.com/luomou97/NLP_for_ARINC653/blob/main/Ontology/Ontology%20Statistics2.jpg)

This is an integration of two models Ontology_NLP and Ontology_HE. **Ellipse nodes (representing entities) in black color denote the overlapping parts; nodes in green color denote the unique necessary parts of Ontology_NLP; nodes in red color (and blue) denote the unique necessary (and unnecessary) parts of Ontology_HE, respectively**. The unnecessary means that the corresponding entities are instanced from enum type attributes, such as the QueuingSrcPort is a Port instance of its enum type attributes PortMode{Queuing, Sampling} and PortDirection{Descination, Source}.
![image](https://github.com/luomou97/NLP_for_ARINC653/blob/main/Ontology/Ontology.jpg)
