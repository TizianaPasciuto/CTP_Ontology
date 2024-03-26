# Competency_Questions

## CQ1
What is a Thematic Paths?  
Che cosa è un percorso tematico?  

Answer: A thematic path is a tool for the enjoyment of cultural heritage that allows to connect cultural objects of different nature (tangible and intangible) through the identification of common themes.  
The chosen theme, which may concern specific topics, contexts, events, places, historical periods or characters and so on, is expressed synthetically by a title and in-depth with a written descriptive text; they can be further identified through subjects.  
The thematic path could be structured either as a collector of cultural objects, without establishing an order of priority, or present a predetermined order.  
The development and use of this enjoyment strategy can be profitable to convey messages and cultural, ethical and social values.  


## CQ2
What is the theme/What are the themes of the path X?  
Quale è la tematica/Quali sono le tematiche del percorso X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?Theme  
WHERE{  
  ?ThematicPath ctp:hasTheme ?Theme.  
}  
LIMIT 10  

## CQ3
Where are cultural objects connected to thematic route X usually kept?  
Dove sono solitamente conservati gli oggetti culturali connessi al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?CulturalResource ?Agent ?Place  
WHERE{  
  ?ThematicPath ctp:hasPart ?CulturalResource.  
  ?CulturalResource ctp:isPreservedBy ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role FILTER regex(?Role, "holder", "i").  
  ?RelationToAgent ctp:involves ?Agent.  
  ?Agent ctp:hasPlace ?Place.  
}  
LIMIT 10  

## CQ4
To which historical period does thematic path X refer?  
A quale periodo storico fa riferimento il percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?TemporalEntity  
WHERE{  
  ?ThematicPath ctp:refersToTemporalEntity ?TemporalEntity.  
}  
LIMIT 10  

## CQ5
By whom were the objects of the thematic path X made?  
Da chi sono stati realizzati gli oggetti del percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?CulturalResource ?Agent  
WHERE{  
  ?ThematicPath ctp:hasPart ?CulturalResource.  
  ?CulturalResource ctp:hasRelationToAgent ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role FILTER regex(?Role, "creator", "i").  
  ?RelationToAgent ctp:involves ?Agent.  
}  
LIMIT 10  

## CQ6
By whom and when were the objects belonging to the thematic path X made?  
Da chi e quando sono stati realizzati gli oggetti appartenenti al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?CulturalResource ?Agent  
WHERE{  
{ ?ThematicPath ctp:hasPart ?CulturalResource.  
  ?CulturalResource ctp:hasRelationToAgent ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role FILTER regex(?Role, "creator", "i").  
  ?RelationToAgent ctp:involves ?Agent.}  

UNION  

{ ?ThematicPath ctp:hasPart ?CulturalResource.  
  ?CulturalResource ctp:hasTime ?TemporalEntity.}  
}  
LIMIT 10  

## CQ7
When were the objects linked to the thematic path X made?  
Quando sono stati realizzati gli oggetti collegati al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?CulturalResource ?TemporalEntity  
WHERE{  
  ?ThematicPath ctp:hasPart ?CulturalResource.  
  ?CulturalResource ctp:hasTime ?TemporalEntity.  
}  
LIMIT 10  

## CQ8
To which agent is the thematic path X inspired by?  
A quale agente è ispirato il percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?Agent  
WHERE{  
  ?ThematicPath ctp:isInspiredByAgent ?Agent.  
}  
LIMIT 10  

## CQ9
Which cultural resources are part of more than one thematic path?  
Quali risorse culturali sono parte di più percorsi tematici?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT *  
WHERE{  
  ?CulturalResource ctp:isPartOf ?ThematicPath FILTER regex(?ThematicPath, {2,}, "i").   
}  
LIMIT 10  

## CQ10
Which thematic paths have been created by the same agent?  
Quali percorsi tematici sono stati realizzati dallo stesso agente?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?Agent ?Role  
WHERE{  
  ?ThematicPath ctp:hasRelationToAgent ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role FILTER regex(?Role, "creator", "i").  
  ?RelationToAgent ctp:involves ?Agent.  
}  
LIMIT 10  

## CQ11
Which thematic paths have been funded by the same agent?  
Quali percorsi tematici sono stati finanziati dallo stesso agente?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?Agent ?Role  
WHERE{  
  ?ThematicPath ctp:hasRelationToAgent ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role FILTER regex(?Role, "funder", "i").  
  ?RelationToAgent ctp:involves ?Agent.  
}  
LIMIT 10  

## CQ12
Which types of cultural heritage are present in the thematic path X?  
Quali tipologie di beni culturali sono presenti in un percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT *  
WHERE{  
  ?ThematicPath ctp:hasPart ?CulturalResource.  
  ?CulturalResource ctp:hasType ?Type.  
}  
LIMIT 10  

## CQ13
Which thematic paths can be identified through the subject "XYZ"?  
Quali percorsi tematici sono individuabili attraverso il soggetto "XYZ"?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?Subject ?ThematicPath  
WHERE{  
  ?ThematicPath ctp:hasSubject ?Subject.  
}  
LIMIT 10  


## CQ14
Which are the places related to the thematic path X?  
Quali sono i luoghi legati al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?Place  
WHERE{  
  ?ThematicPath ctp:refersToPlace ?Place.  
}  
LIMIT 10  


## CQ15
Which cultural, ethical and social values does the thematic path X want to convey?  
Quali valori culturali, etici e sociali vuole trasmettere il percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?rdfs  
WHERE{  
  ?ThematicPath ctp:conveys ?rdfs.  
}  
LIMIT 10  


## CQ16
Which sorting is used to arrange the cultural objects in the thematic path X?  
In che ordine sono disposti gli oggetti culturali nel percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT *  
WHERE{  
  ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
  ?OrderedListSlot ctp:hasItem ?CulturalResource.  
  ?OrderedListSlot ctp:hasIndex ?rdfs.  
}  
LIMIT 10  


## CQ17
The thematic path X is realized in one or more events (i.e. virtual or physical exhibition)? Which one/s?  
Il percorso tematico X è legato a uno o più eventi (per esempio mostra virtuale, mostra fisica)? Quale/i?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT *  
WHERE{  
  ?ThematicPath ctp:isRealizedIn ?CulturalEvent.  
  ?CulturalEvent ctp:hasTime ?TemporalEntity.  
}  
LIMIT 10  


## CQ18
The thematic path X is composed by one or more sub-thematic paths (i.e. exhibitions' sub-paths)?  
Il percorso tematico X è composto da uno o più sotto percorsi tematici (per esempio sottofiloni tematici di una mostra)?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?ThematicPath  
WHERE{  
  ?ThematicPath ctp:includes ?ThematicPath.  
}  
LIMIT 10  

## CQ19
How is it possible to access the thematic path X?  
Come è possibile accedere al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?rdfs   
WHERE{  
  ?ThematicPath ctp:linkToResource ?rdfs  
}  
LIMIT 10  

## CQ20
Where can cultural resources related to the thematic path X be viewed?
Dove sono visualizzabili gli oggetti legati al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?CulturalResource ?ThematicPath ?rdfs   
WHERE{  
  ?CulturalResource ctp:isPartOf ?ThematicPath.  
  ?CulturalResource ctp:linkToResource ?rdfs.  
}  
LIMIT 10  

## CQ21
Which cultural resources are linked to the thematic path X?  
Quali risorse culturali sono collegate al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT *  
WHERE{  
  ?CulturalResource ctp:isPartOf ?ThematicPath.  
}  
LIMIT 10  

## CQ22
Where is it possible to buy products related to the thematic path X?  
Dove è possibile acquistare prodotti relativi al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?Product ?Type ?rdfs  
WHERE{  
  ?ThematicPath ctp:allowsTheSaleOf ?Product.  
  ?Product ctp:isSelledBy ?rdfs.  
  ?Product ctp:hasTitle ?rdfs.  
  ?Product ctp:hasType ?Type.  
}  
LIMIT 10  

## CQ23
Which is the identification code associated with the cultural resource X by holder X ?  
Qual è il codice identificativo associato alla risorsa culturale X dall'agente X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?CulturalResource ?Identifier ?Agent  
WHERE{  
  ?CulturalResource ctp:hasSecondaryIdentifier ?Idenfier.  
  ?Identifier ctp:hasCreator ?Agent.  
}  
LIMIT 10  

## CQ24
Which is the internal identifier of the resource X in the XY catalog?  
Qual è l'identificativo interno della risorsa X nel catalogo XY?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?CulturalResource ?rdfs  
WHERE{  
  ?CulturalResource ctp:hasPrimaryIdentifier ?rdfs.  
}  
LIMIT 10  

## CQ25
Which thematic routes have been created in the year XX?  
Quali percorsi tematici sono stati creati nell'anno XX?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPath ?xsd  
WHERE{  
  ?ThematicPath ctp:hasCreationDate ?xsd.  
}  
LIMIT 10  