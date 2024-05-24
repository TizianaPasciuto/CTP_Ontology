# Competency_Questions

## CQ1
What is a Thematic Paths?  
Che cosa è un percorso tematico?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
SELECT ?Definition  
WHERE{  
  ctp:ThematicPath rdfs:comment ?Definition.  
  #FILTER(LANG(?Definition) ="en").  
}  
LIMIT 10  

## CQ2
What is the theme/What are the themes of the path X?  
Quale è la tematica/Quali sono le tematiche del percorso X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?ThemeTitle ?ThemeDescription  
WHERE {  
    ?ThematicPath ctp:hasTheme ?Theme.  
    ?ThematicPath ctp:hasTitle ?ThematicPathTitle.  
    ?Theme ctp:hasTitle ?ThemeTitle.  
    ?Theme ctp:hasDescription ?ThemeDescription.  
    FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
    #FILTER(LANGMATCHES(LANG(?ThematicPathTitle), 'en') &&  
           #LANGMATCHES(LANG(?ThemeTitle), 'en') &&  
           #LANGMATCHES(LANG(?ThemeDescription), 'en'))  
}  
GROUP BY ?ThematicPathTitle ?ThemeTitle ?ThemeDescription  
LIMIT 100  

## CQ3
Where are cultural objects connected to thematic route X usually kept?  
Dove sono solitamente conservati gli oggetti culturali connessi al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?CulturalResourceTitle ?PlaceName  
WHERE{  
  {  
    ?ThematicPath ctp:hasPart ?CulturalResource.  
  }  
  UNION  
  {  
    ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
    ?OrderedListSlot ctp:hasItem ?CulturalResource.  
  }  
  ?CulturalResource ctp:isPreservedBy ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role.  
  ?Role rdfs:label ?Holder.  
  ?RelationToAgent ctp:involves ?Agent.  
  ?Agent ctp:hasPlace ?Place.  
  Optional{?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  Optional{?Place ctp:hasTitle ?PlaceName}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
GROUP BY ?ThematicPathTitle ?CulturalResourceTitle ?PlaceName  
LIMIT 100  

## CQ4
To which historical period does thematic path X refer?  
A quale periodo storico fa riferimento il percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?TemporalEntityLabel  
WHERE{  
  ?ThematicPath ctp:refersToTemporalEntity ?TemporalEntity.  
  Optional{?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?TemporalEntity rdfs:label ?TemporalEntityLabel}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
  #FILTER(  
    #LANGMATCHES(LANG(?ThematicPathTitle),'en') && LANGMATCHES(LANG(?TemporalEntityLabel),'en'))  
}  
LIMIT 100  

## CQ5
By whom were the objects of the thematic path X made?  
Da chi sono stati realizzati gli oggetti del percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?CulturalResourceTitle ?AgentName  
WHERE{  
  {  
    ?ThematicPath ctp:hasPart ?CulturalResource.  
  }  
  UNION  
  {  
    ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
    ?OrderedListSlot ctp:hasItem ?CulturalResource.  
  }  
  ?CulturalResource ctp:hasRelationToAgent ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role.  
  ?Role rdfs:label ?Creator.  
  ?RelationToAgent ctp:involves ?Agent.  
  Optional{?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  Optional{?Agent ctp:hasName ?AgentName}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
  FILTER(BOUND(?AgentName))  
}  
LIMIT 100  

## CQ6
By whom and when were the objects belonging to the thematic path X made?  
Da chi e quando sono stati realizzati gli oggetti appartenenti al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?CulturalResourceTitle ?AgentName ?CulturalResourceDate  
WHERE{  
  {  
    {  
      ?ThematicPath ctp:hasPart ?CulturalResource.  
    }  
    UNION  
    {  
      ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
      ?OrderedListSlot ctp:hasItem ?CulturalResource.  
    }  
  }  
  Optional{?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  {  
    {  
      ?CulturalResource ctp:hasRelationToAgent ?RelationToAgent.  
      ?RelationToAgent ctp:hasRole ?Role.  
      ?Role rdfs:label ?Creator.  
      ?RelationToAgent ctp:involves ?Agent.  
      Optional{?Agent ctp:hasName ?AgentName}.  
    }  
    UNION  
    {  
      ?CulturalResource ctp:hasTime ?TemporalEntity.  
      ?TemporalEntity ctp:hasDate  ?CulturalResourceDate.  
    }  
  }  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ7
When were the objects linked to the thematic path X made?  
Quando sono stati realizzati gli oggetti collegati al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPathTitle ?CulturalResourceTitle ?CulturalResourceDate  
WHERE{  
   {  
    ?ThematicPath ctp:hasPart ?CulturalResource.  
  }  
  UNION  
  {  
    ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
    ?OrderedListSlot ctp:hasItem ?CulturalResource.  
  }  
  ?CulturalResource ctp:hasTime ?TemporalEntity.  
  ?TemporalEntity ctp:hasDate  ?CulturalResourceDate.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
GROUP BY ?ThematicPathTitle ?CulturalResourceTitle ?CulturalResourceDate  
LIMIT 100  

## CQ8
To which agent is the thematic path X inspired by?  
A quale agente è ispirato il percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPathTitle ?AgentName  
WHERE{  
  ?ThematicPath ctp:isInspiredByAgent ?Agent.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}. 
  Optional{ ?Agent ctp:hasName ?AgentName}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100   

## CQ9
Which cultural resources are part of more than one thematic path?  
Quali risorse culturali sono parte di più percorsi tematici?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?CulturalResourceTitle (COUNT(?ThematicPath) AS ?PathCount)  
WHERE{  
  ?CulturalResource ctp:isPartOf ?ThematicPath.  
  Optional{ ?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
}  
GROUP BY ?CulturalResourceTitle  
HAVING (?PathCount > 1)  
LIMIT 100  

## CQ10
Which thematic paths have been created by the same agent?  
Quali percorsi tematici sono stati realizzati dallo stesso agente?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
PREFIX rdf: ```<http://www.w3.org/1999/02/22-rdf-syntax-ns#>```  
SELECT ?ThematicPathTitle  
WHERE {  
  ?ThematicPath rdf:type ctp:ThematicPath.  
  ?ThematicPath ctp:hasRelationToAgent ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role.  
  ?RelationToAgent ctp:involves ?Agent.  
  OPTIONAL { ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  OPTIONAL { ?Role rdfs:label ?RoleLabel}.  
  OPTIONAL { ?Agent ctp:hasName "InsertNameHere"}.  
  FILTER regex(?RoleLabel, "creator", "i").  
  }  
LIMIT 100  

## CQ11
Which thematic paths have been funded by the same agent?  
Quali percorsi tematici sono stati finanziati dallo stesso agente?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle  
WHERE {  
  ?ThematicPath ctp:hasRelationToAgent ?RelationToAgent.  
  ?RelationToAgent ctp:hasRole ?Role.  
  ?RelationToAgent ctp:involves ?Agent.  
  OPTIONAL { ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  OPTIONAL { ?Role rdfs:label ?RoleLabel}.  
  OPTIONAL { ?Agent ctp:hasName "InsertNameHere"}.  
  FILTER regex(?RoleLabel, "funder", "i").  
}  
LIMIT 100  

## CQ12
Which types of cultural heritage are present in the thematic path X?  
Quali tipologie di beni culturali sono presenti in un percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?CulturalResourceTitle ?CulturalResourceType  
WHERE{  
  {  
    ?ThematicPath ctp:hasPart ?CulturalResource.  
  }  
  UNION  
  {  
    ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
    ?OrderedListSlot ctp:hasItem ?CulturalResource.  
  }  
  ?CulturalResource ctp:hasType ?Type.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  Optional{ ?Type rdfs:label ?CulturalResourceType}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ13
Which thematic paths can be identified through the subject "XYZ"?  
Quali percorsi tematici sono individuabili attraverso il soggetto "XYZ"?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?SubjectLabel ?ThematicPathTitle  
WHERE{  
  ?ThematicPath ctp:hasSubject ?Subject.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?Subject rdfs:label ?SubjectLabel}.  
  FILTER(?SubjectLabel = "InsertSubjectHere"@LANG).  
}  
LIMIT 100  

## CQ14
Which are the places related to the thematic path X?  
Quali sono i luoghi legati al percorso tematico X?  

PREFIX ctp: <https://w3id.org/ctp#>  
SELECT ?ThematicPathTitle ?PlaceName  
WHERE{  
  ?ThematicPath ctp:refersToPlace ?Place.  
  Optional{ ?Place ctp:hasTitle ?PlaceName}.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ15
Which cultural, ethical and social values does the thematic path X want to convey?  
Quali valori culturali, etici e sociali vuole trasmettere il percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPathTitle ?Message  
WHERE{  
  ?ThematicPath ctp:conveys ?Message.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ16
Which sorting is used to arrange the cultural objects in the thematic path X?  
In che ordine sono disposti gli oggetti culturali nel percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?CulturalResourceTitle ?Index  
WHERE{  
  ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
  ?OrderedListSlot ctp:hasItem ?CulturalResource.  
  ?OrderedListSlot ctp:hasIndex ?Index.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
ORDER BY ?Index  
LIMIT 100  

## CQ17
The thematic path X is realized in one or more events (i.e. virtual or physical exhibition)? Which one/s?  
Il percorso tematico X è legato a uno o più eventi (per esempio mostra virtuale, mostra fisica)? Quale/i?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPathTitle ?CulturalEventTitle  ?CulturalEventDate  
WHERE{  
  ?ThematicPath ctp:isRealizedIn ?CulturalEvent.  
  ?CulturalEvent ctp:hasTime ?TemporalEntity.  
  ?TemporalEntity ctp:hasDate ?date.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?CulturalEvent ctp:hasTitle ?CulturalEventTitle}.  
  Optional{ ?TemporalEntity ctp:hasDate ?CulturalEventDate}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ18
The thematic path X is composed by one or more sub-thematic paths (i.e. exhibitions' sub-paths)?  
Il percorso tematico X è composto da uno o più sotto percorsi tematici (per esempio sottofiloni tematici di una mostra)?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdf: ```<http://www.w3.org/1999/02/22-rdf-syntax-ns#>```  
SELECT ?ThematicPathTitle ?SubThematicPathTitle  
WHERE{  
  ?ThematicPath rdf:type ctp:ThematicPath.  
  ?ThematicPath ctp:includes ?SubThematicPath.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?SubThematicPath ctp:hasTitle ?SubThematicPathTitle}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ19
How is it possible to access the thematic path X?  
Come è possibile accedere al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPathTitle ?Link  
WHERE{  
  ?ThematicPath ctp:linkToResource ?Link  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ20
Where can cultural resources related to the thematic path X be viewed?
Dove sono visualizzabili gli oggetti legati al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?CulturalResourceTitle ?ThematicPathTitle ?Link  
WHERE{  
  ?CulturalResource ctp:isPartOf ?ThematicPath.  
  ?CulturalResource ctp:linkToResource ?Link.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ21
Which cultural resources are linked to the thematic path X?  
Quali risorse culturali sono collegate al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?CulturalResourceTitle ?ThematicPathTitle  
WHERE{  
 {  
    ?ThematicPath ctp:hasPart ?CulturalResource.  
  }  
  UNION  
  {  
    ?ThematicPath ctp:hasSlot ?OrderedListSlot.  
    ?OrderedListSlot ctp:hasItem ?CulturalResource.  
  }  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.   
  FILTER(?ThematicPathTitle = "InserTitleHere"@LANG).  
}  
LIMIT 100  

## CQ22
Where is it possible to buy products related to the thematic path X?  
Dove è possibile acquistare prodotti relativi al percorso tematico X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
SELECT ?ThematicPathTitle ?ProductTitle ?ProductType ?Link  
WHERE{  
  ?ThematicPath ctp:allowsTheSaleOf ?Product.  
  ?Product ctp:isSelledBy ?Link.  
  ?Product ctp:hasTitle ?ProductTitle.  
  ?Product ctp:hasType ?Type.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  Optional{ ?Type rdfs:label ?ProductType}.  
  FILTER(?ThematicPathTitle = "InsertTitleHere"@LANG).  
}  
LIMIT 100  

## CQ23
Which is the identification code associated with the cultural resource X by holder X ?  
Qual è il codice identificativo associato alla risorsa culturale X dall'agente X?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdfs: ```<http://www.w3.org/2000/01/rdf-schema#>```  
PREFIX rdf: ```<http://www.w3.org/1999/02/22-rdf-syntax-ns#>```  
SELECT ?IdentifierNumber ?CulturalResourceTitle ?AgentName  
WHERE{  
  ?CulturalResource rdf:type ctp:CulturalResource.  
  ?CulturalResource ctp:hasTitle "InsertCulturalResourceTitleHere"@LANG.  
  ?CulturalResource ctp:hasSecondaryIdentifier ?Identifier.  
  ?Identifier ctp:hasNotation ?IdentifierNumber.  
  Optional{ ?CulturalResource ctp:hasTitle ?CulturalResourceTitle}.  
  Optional{ ?Organization rdfs:label ?AgentName}.  
  FILTER(?AgentName = "InsertAgentNameHere"@LANG).  
}  
GROUP BY ?IdentifierNumber ?CulturalResourceTitle ?AgentName  
LIMIT 100  

## CQ24
Which is the internal identifier of the resource X in the XY catalog?  
Qual è l'identificativo interno della risorsa X nel catalogo XY?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
PREFIX rdf: ```<http://www.w3.org/1999/02/22-rdf-syntax-ns#>```  
SELECT ?IdentifierNumber  
WHERE{  
  ?CulturalResource rdf:type ctp:CulturalResource.  
  ?CulturalResource ctp:hasTitle "InsertCulturalResourceTitleHere"@LANG.  
  ?CulturalResource ctp:hasPrimaryIdentifier ?IdentifierNumber.  
}  
LIMIT 100  

## CQ25
Which thematic routes have been created in the year XX?  
Quali percorsi tematici sono stati creati nell'anno XX?  

PREFIX ctp: ```<https://w3id.org/ctp#>```  
SELECT ?ThematicPathTitle ?Date  
WHERE{  
  ?ThematicPath ctp:hasCreationDate ?Date.  
  Optional{ ?ThematicPath ctp:hasTitle ?ThematicPathTitle}.  
  FILTER (?Date >= "2024-01-01"^^<http://www.w3.org/2001/XMLSchema#date> && ?Date <="2024-12-31"^^<http://www.w3.org/2001/XMLSchema#date>)  
}  
LIMIT 100  