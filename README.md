
# Projet d'Ontologie : Domaine des Voitures 🚗

Ce projet vise à modéliser une ontologie complète dans le domaine des voitures, en suivant les cinq phases décrites ci-dessous.  
**Dépôt GitHub** : [Lien vers le dépôt](https://github.com/MohamedYassineAbid/Sementique_I1)

---

## Phase 1 : Choix du Domaine  
### **Domaine Sélectionné** : **Automobile**  
**Justification** :  
- Les voitures jouent un rôle central dans la société moderne, avec des caractéristiques techniques et commerciales complexes.  
- Une ontologie permet de structurer les relations entre marques, modèles, équipements, et pays d'origine, facilitant des requêtes avancées.  

**Concepts Clés** :  
- **Marque** (ex: Audi, Renault)  
- **Modèle** (ex: R8, Clio)  
- **Type** (ex: Sportive, Familiale, Luxe)  
- **Pays** (ex: Allemagne, France)  
- **Équipement** (ex: Nombre de sièges)  
- **Prix** (attribut numérique).  

---

## Phase 2 : Modélisation en RDF/RDFS  
### **Namespaces Utilisés** :  
```turtle
@prefix voiture: <http://www.semanticweb.org/ontologie-voiture#>  
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>  
@prefix owl: <http://www.w3.org/2002/07/owl#>  
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>  
```

### **Classes et Propriétés** :
```turtle
# Classes
voiture:Marque a owl:Class .  
voiture:Modele a owl:Class .  
voiture:Equipement a owl:Class .  

# Propriétés
voiture:aPaysOrigine a owl:ObjectProperty ;  
    rdfs:domain voiture:Marque ;  
    rdfs:range voiture:Pays .  

voiture:prix a owl:DatatypeProperty ;  
    rdfs:domain voiture:Modele ;  
    rdfs:range xsd:integer .  
```

---

## Phase 3 : Interrogation avec SPARQL  
### Requêtes Exemple :  

**Lister les marques allemandes** :
```sparql
PREFIX voiture: <http://www.semanticweb.org/ontologie-voiture#>  
SELECT ?marque  
WHERE {  
    ?marque rdfs:subClassOf voiture:MarqueAllemande .  
}  
```
**Résultat** : Audi, Mercedes, Smart.

**Afficher les modèles de luxe (prix ≥ 100 000 €)** :
```sparql
PREFIX voiture: <http://www.semanticweb.org/ontologie-voiture#>  
SELECT ?modele  
WHERE {  
    ?modele rdfs:subClassOf voiture:Luxe .  
}  
```
**Résultat** : Sportive.

**Trouver les équipements disponibles** :
```sparql
PREFIX voiture: <http://www.semanticweb.org/ontologie-voiture#>  
SELECT ?equipement  
WHERE {  
    ?equipement rdfs:subClassOf voiture:Equipement .  
}  
```
**Résultat** : NombreSieges.

**Modèles de Renault** :
```sparql
PREFIX voiture: <http://www.semanticweb.org/ontologie-voiture#>  
SELECT ?modele  
WHERE {  
    ?modele rdfs:subClassOf [  
        a owl:Restriction ;  
        owl:onProperty voiture:aMarque ;  
        owl:allValuesFrom voiture:Renault  
    ] .  
}  
```
**Résultat** : Clio, Master.

---

## Phase 4 : Développement en OWL  
### **Formalisation des Concepts :**  
#### Restrictions :  
```turtle
voiture:Sportive a owl:Class ;  
    equivalentClass [  
        a owl:Class ;  
        owl:intersectionOf (  
            voiture:Voiture  
            [ a owl:Restriction ;  
              owl:onProperty voiture:estEquipeDe ;  
              owl:allValuesFrom voiture:DeuxSieges  
            ]  
        )  
    ] .  
```

### **Avantages par rapport aux Bases de Données Relationnelles** :  
- **Inférence** : Détection automatique de relations (ex: R8 est une VoitureAllemande).  
- **Flexibilité** : Ajout dynamique de classes et propriétés sans modifier le schéma.  

---

## Phase 5 : Règles SWRL  
### **Règles Ajoutées** :  
```turtle
Voiture(?v) ^ estEquipeDe(?v, ?s) ^ DeuxSieges(?s) ^ prix(?v, ?p) ^ swrlb:greaterThan(?p, 50000) → Sportive(?v)

---

## Installation et Utilisation  
- **Ouvrir l'ontologie** : Utilisez Protégé (https://protege.stanford.edu/).  
- **Exécuter les requêtes** : Via l'onglet SPARQL Query dans Protégé.  
- **Activer le Reasoner** : HermiT pour les inférences.
