# CTP_Ontology  
## Cultural Thematic Path Ontology - An ontology to travel in culture  
This repository is dedicated to the development of an ontological module on the creation of cultural thematic path related to the GLAM (Galleries, Libraries, Archives, and Museum) domain, serving as a tool to "travel" through the cultural heritage by allowing the linking between cultural resources, of various types and stored in different places, unified by one or more themes.  
The ontological module aims to be autonomous yet easily reusable with other existing domain ontologies, widely used in the GLAM sector.  
The ontology can be found [here](https://github.com/TizianaPasciuto/CTP_Ontology/blob/f43eece9c202ff75ac3054c2f89a5f859ea5c56d/documentation/index-en.html).  

## Development  
The development of the ontology on Cultural Thematic Paths follows the Linked Open Terms (LOT) methodology, as outlined by [Poveda-Villalón et al.](https://www.sciencedirect.com/science/article/pii/S0952197622000525)  

### Ontology requirements specification
This activity comprises the collection of requirements that the ontology should satisfy. The fundamental phases consist of **(I) identifying scenarios**, which are situations in which the ontology can be used, **(II) specifying the purpose and scope** within which ontology operates and produce a **(III) set of functional requirements**.  

First of all, **(I) 3 scenarios** have been selected:  
**1. Exhibition "Transitions | enterprise - work - society":** The purpose of this scenario is to keep the memory alive of the exhibition "Transitions | enterprise - work - society", organized by the Ansaldo Foundation and held at the Falcone Theater of the Royal Palace of Genoa from 22 February to 25 April 2023. The exhibition recounted the evolution of three interconnected sub-thematic paths (enterprise, work, and society) associated with the development of the Ansaldo Company, spanning from its inception in the early 1850s to the present day.  
**Actors:** Genoese citizens, tourists, scholars.  
**2. DigitXL - Novum Corpus Fontanianum:** This scenario aims to celebrate the legacy of the scientist Felice Fontana by compiling his professional works into a comprehensive _"opera omnia"_ available to both the scientific community and the general public. As prominent figure in the Italian and European scientific research community during the 18th and 19th centuries, Fontana conducted studies across various natural science fields, pioneering cutting-edge methods, models, and analytical tools.  
**Actors:** Scholars (especially of the history of science), students, tourists.  
**3. Cultural Routes - Camino de Santiago:** The following scenario aims to promote the fundamental principles and foundational values of European culture through the establishment of cultural itineraries. These itineraries are not merely physical routes but genuine channels for intercultural dialogue, serving as a means to overcome geographic barriers and historical differences. Cultural itineraries become a vehicle for a deeper understanding of European history, creating a bridge between the past and the present.  
**Actors:** Pilgrims, tourists.  

In reference to the ontology's **(II) purpose**, the development of an ontology for thematic paths aims not only to provide a clear and comprehensive definition of the concept but also to specify its main and basic requirements and the organization of content.  
The main purpose is to facilitate the enhancement of cultural heritage by facilitating user navigation through a series of described and interconnected information and resources. This achievement can be attained through the development of an ontology that serves as a tool for the organization, management, exchange, and enjoyment of online information.  
With regard to the **(II) scope**, although the structuring of thematic paths can be related to any sector, in this study the attention will be focused on the GLAM domain. Therefore, the reference scope will be related to the cultural heritage.  

To identify **(III) a set of functional requirements** of the ontology, it is possible to materialize them into one or more forms. In this case, have been selected:  
**[1. Competency Questions (CQs):](https://github.com/TizianaPasciuto/CTP_Ontology/blob/0fdd8bbd03df998c3dd2aa1b1a311f9b798a6108/Competency_Questions.md)** a set of queries that the ontology to be developed should answer;  
**[2. Tabular information:](https://docs.google.com/spreadsheets/d/1qAHCUKAJaNcs_p7jHjx3pVr0d7cdsuijOhjfuWuraPA/edit?usp=sharing)** information structured into 3 types of tables:  
    ***a. Concepts:*** identify and define entities;  
    ***b. Relations:*** group all the relations between concepts;  
    ***c. Attributes:*** group all related attributes under the relevant concepts.  

### Ontology implementation
The activity concerns the construction of the ontology using a formal language, generating as output a version of the ontology itself.  

The first phase is the **(I) ontology conceptualization**, which is achieved by creating a model representing the ontology's domain. The [CTP ontology model](https://github.com/TizianaPasciuto/CTP_Ontology/blob/a0c530ce6cd49e77ff99eedfaa4a6e9a3f215695/Conceptualization_TPs_20240306-Schema%2006.03.2024.drawio.png) has been developed using [Graffoo](https://essepuntato.it/graffoo), where all relationships, entities, and attributes identified in previous stages are synthesized. Among the various modeling choices that can be implemented during conceptualization, a useful solution for some recurring modeling problems is the use of an **[Ontology Design Pattern (ODP)](http://ontologydesignpatterns.org/)**, that is a reusable solution implemented by other ontology developers.  

The next phase involves **(II) ontology encoding**, so the ontology must be produced in an implementation language; to achieve this, the [Protégé ontology editor](https://protege.stanford.edu) was used.  

The last phase of this activity involves the **(III) Ontology evaluation**, that refers to checking the technical quality of the ontology.  

### Ontology publication ###
The activity provides to make the ontology accessible both as a human-readable documentation and a machine-readable file from its URI.  
The documentation for the Cultural Thematic Path Ontology is realized using [WIDOCO - WIzard for DOCumenting Ontologies](https://github.com/dgarijo/Widoco).  

### Ontology maintenance ###
The objective of this activity is to update the ontology during its life cycle, detecting bugs and new requirements.  