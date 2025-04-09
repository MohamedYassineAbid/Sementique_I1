# Car Ontology

This repository contains an OWL file representing a car ontology. The ontology includes classes, properties, and individuals related to cars, brands, types, and equipment. It provides a detailed representation of the automobile domain using equivalence axioms, subclass relationships, and domain-specific constraints.

---

## Ontology Domain: Automobile Industry

The ontology models the domain of automobiles, focusing on car brands, models, types, countries of origin, and equipment. It aims to enable semantic reasoning about cars based on features such as type, cost, and equipment.

### Justification for Domain Choice
- **Structured**: The automobile domain has clear entities and relationships (e.g., brands, models, types).
- **Relevant**: Automobiles are integral to transportation, economy, and personal mobility.
- **Rich in Data**: Automotive datasets are available from manufacturers and research entities.
- **Practical**: The ontology supports applications in e-commerce, research, and recommendation systems.

---

## Namespaces Used

| Prefix | URI                                                   |
|--------|-------------------------------------------------------|
| rdf    | http://www.w3.org/1999/02/22-rdf-syntax-ns#          |
| rdfs   | http://www.w3.org/2000/01/rdf-schema#               |
| owl    | http://www.w3.org/2002/07/owl#                      |
| xsd    | http://www.w3.org/2001/XMLSchema#                   |
| :      | http://www.semanticweb.org/gleroy/ontologies/2018/9/car-ontology# |

The namespaces ensure compliance with semantic web standards and facilitate extensibility.

---

## Classes and Properties

### Key Classes
1. **Car**: Represents automobiles.
2. **Brand**: Defines car manufacturers (e.g., Audi, Renault).
3. **Model**: Specifies specific car versions (e.g., Clio, R8).
4. **Type**: Categorizes cars (e.g., Familial, Sportive, Luxury).
5. **Country**: Represents countries of origin (e.g., France, Germany).
6. **Equipment**: Details features like `NumberOfSeats`.

### Subclasses
- **Type**: Includes subclasses like Familial and Luxury, based on specific conditions.

### Object Properties
| Name               | Domain      | Range          |
|--------------------|-------------|----------------|
| hasBrand           | Car         | Brand          |
| isEquipedWith      | Car         | Equipment      |
| hasCountryOfOrigin | Brand       | Country        |

### Data Properties
| Name     | Domain | Data Type   |
|----------|--------|-------------|
| cost     | Car    | xsd:integer |

---

## SPARQL Queries

### Query 1: Retrieve all German Cars and their Brands

```sparql
PREFIX : <http://www.semanticweb.org/gleroy/ontologies/2018/9/car-ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?car ?brand WHERE {
  ?car rdf:type :GermanCar .
  ?car :hasBrand ?brand .
}
```

This query identifies cars produced by German brands and links each car to its manufacturer.

### Query 2: List Cars with Specific Types

```sparql
PREFIX : <http://www.semanticweb.org/gleroy/ontologies/2018/9/car-ontology#>

SELECT ?car ?type WHERE {
  ?car rdf:type :Car .
  ?car :hasType ?type .
}
```

This query retrieves cars and their corresponding types (e.g., Familial, Luxury).

---

## Screenshots

### 1. Ontology Classes
![Classes Screenshot](https://github.com/MohamedYassineAbid/Sementique_I1/blob/main/Screenshots/Screenshot%20from%202025-04-09%2016-42-21.png)
### 2. Object Properties
![Object Properties Screenshot](https://github.com/MohamedYassineAbid/Sementique_I1/blob/main/Screenshots/Screenshot%20from%202025-04-09%2016-46-42.png)

### 3. Data Properties
![Data Properties Screenshot](https://github.com/MohamedYassineAbid/Sementique_I1/blob/main/Screenshots/Screenshot%20from%202025-04-09%2016-46-46.png)

### 4. Individuals
![Individuals Screenshot](https://github.com/MohamedYassineAbid/Sementique_I1/blob/main/Screenshots/Screenshot%20from%202025-04-09%2016-46-56.png)

---

## Conclusion

The ontology provides a robust framework for representing and reasoning about the automobile domain. It simplifies querying and analysis, enhances semantic understanding, and facilitates knowledge sharing across applications. The use of SPARQL queries demonstrates its practical applications in semantic reasoning and intelligent systems.
