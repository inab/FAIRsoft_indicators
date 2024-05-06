# I1. Data Format Standards and Practices 

Whether the software adheres to data format standards and its operational practices concerning data handling it encompasses standard formats and APIs, the flexibility and verifiability of these formats, and the tracking of data provenance. 

Adhering to data format standards and robust data handling practices is critical for ensuring interoperability and reliability across systems, enhancing software integration, maintaining data integrity, and supporting traceability, which boosts user trust and system efficiency.


--- 


## I1.1. Use of standard data formats

### What is being measured? 

- Whether the input and output data types are formally specified and related to accepted ontologies. 

### Why should we measure it? 

- Using standard data formats minimises the need for error-prone and resource-intensive transformations to meet unique software input requirements. It facilitates collective efforts to develop high-quality data management tools, reducing reliance on ad hoc data transformations. 

### How do we measure it? 

- At least one input or output data format specified in the EDAM format ontology is considered valid. 

### Types it applies to 

- all

--- 


## I1.2. Use of standard API specification framework 

### What is being measured? 

- Whether APIs (REST, libraries) are documented in a standard framework. 

### Why should we measure it? 

- Documenting APIs in a standard framework ensures they are universally understandable and easily integrable across different platforms and services. 

### How do we measure it? 

- Not measured.

### Types it applies to

- web

---  

## I1.3 Verifiability of data formats 

### What is being measured? 

- Whether input/output data are specified using verifiable schemas. 

### Why should we measure it? 

- Verifiability of data formats is crucial as it allows users to automatically confirm that their data complies with accepted standards, ensuring compatibility and readability by other systems using the same format. This verification reduces errors in data processing and enhances overall system interoperability. 

### How do we measure it? 

- Any standard formats (I1.1) plus JSON, XML, RDF and XDS  are considered valid. 


### Types it applies to

- non-web

--- 

 
## I1.4. Flexibility of data format supported 

### What is being measured? 

- Whether the software allows one to choose among various input/output data formats or provides the necessary mechanisms to convert other standard formats into the supported ones. 

### Why should we measure it? 

- Supporting various data formats directly in software eliminates the need for data transformations, thereby reducing error points and saving significant time and resources for users, enhancing flexibility and efficiency. 

### How do we measure it? 

- At least two input or output data formats are valid. 

### Types it applies to 

- all

---


## I1.5. Generation of provenance information

### What is being measured? 

- Whether the software provides provenance information according to accepted standards. 

### Why should we measure it? 

- Generating provenance information is crucial for adhering to the FAIR data principles, as it provides detailed documentation that enhances data transparency, traceability, and trustworthiness, thereby supporting improved data management. 

### How do we measure it? 

- Not measured 

### Types it applies to 

- all
