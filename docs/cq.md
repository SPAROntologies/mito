## Competency Questions

MiTO can be used for answering several questions related to mentions in scholarly resources.
In the following subsections, some of them are introduced together with their respective SPARQL queries. 

The prefixes that are used in all the SPARQL queries provided below are defined as follows:

    PREFIX mito: <http://purl.org/spar/mito/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX oa: <http://www.w3.org/ns/oa#>
    PREFIX cnt: <http://www.w3.org/2011/content#>
    PREFIX c4o: <http://purl.org/spar/c4o/>

### CQ1

Which entities are mentioned by a document, along with their types and titles?

    SELECT ?document ?mentionedEntity ?entityType ?entityName
    WHERE {
        ?document mito:mentions ?mentionedEntity .
        ?mentionedEntity a ?entityType .
        OPTIONAL { ?mentionedEntity dcterms:title ?entityName . }
        OPTIONAL { ?mentionedEntity foaf:name ?entityName . }
    }

### CQ2

What are the mentions, their types, and the entities involved?

    SELECT ?mention ?mentioningEntity ?mentionedEntity ?mentionType
    WHERE {
        ?mention a mito:Mention ;
            mito:hasMentioningEntity ?mentioningEntity ;
            mito:hasMentionedEntity ?mentionedEntity ;
            mito:hasMentionType ?mentionType .
    }

### CQ3

What textual comments or annotations target a specific mention?

    SELECT ?mention ?mentionType ?commentText
    WHERE {
        ?mention a mito:Mention ;
            mito:hasMentionType ?mentionType .
        ?annotation a oa:Annotation ;
            oa:hasTarget ?mention ;
            oa:hasBody ?body .
        ?body cnt:chars ?commentText .
    }

### CQ4

Which in-text reference pointers are linked to a mention via annotations?

    SELECT ?pointer ?pointerContent ?mention ?mentionedEntity ?annotator
    WHERE {
        ?pointer a c4o:InTextReferencePointer ;
            c4o:hasContent ?pointerContent .
        ?annotation a oa:Annotation ;
            oa:hasTarget ?pointer ;
            oa:hasBody ?mention .
        ?mention a mito:Mention ;
            mito:hasMentionedEntity ?mentionedEntity .
        OPTIONAL { ?annotation oa:annotatedBy ?annotator . }
    }