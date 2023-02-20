# I1. Documentation on Input/output data types and formats 

- ### I1.1. Usage of standard data formats

    Input and output data types are formally specified and related to accepted ontologies.

    | Why should we measure it?  | How do we measure it? | Types it applies to  |
    |----------------------------|-----------------------|----------------------|
    | Data format transformations to meet software often unique input format requirements are a source of errors and take time and resources. The usage of standard formats by software minimizes the transformations data is subjected to in the course of research. In addition, collective efforts can be made to create good quality tools for the management of data avoiding ad hoc scripting. | At least one input or output data format that is specified in the EDAM format ontology is considered valid. | all | 

- ### I1.2. Usage of standard API framework 

    PIs (Rest, libraries) are documented in a standard framework (OpenAPI, WES...).

    | Why should we measure it?  | How do we measure it? | Types it applies to  |
    |----------------------------|-----------------------|----------------------|
    | The usage of standard frameworks greatly eases their usage | Not measured | non-web |

- ### I1.3 Verifiability of data formats 

    Input and output data formats are specified using verifiable schemas (e.g. XDS, Json schema, ...). 

    | Why should we measure it?  | How do we measure it? | Types it applies to  |
    |----------------------------|-----------------------|----------------------|
    | Verifiability allows users to automatically make sure their data will be readable by other resources supporting that same format. | Standard formats (I1.1) as well as JSON are considered valid. | non-web |

- ### I1.4. Flexibility of data format supported 

    The software accepts various input/output data formats for the same operation, or provide the necessary tools to convert other common formats into the supported ones.

    | Why should we measure it?  | How do we measure it? | Types it applies to  |
    |----------------------------|-----------------------|----------------------|
    | Data format transformation to meet software often unique input format requirements are a source of errors and take time and resources. The capacity of a software to support various formats avoids the need for data transformation by the user. | At least two input or output data formats are valid. | all |


- ### I1.5. Generation of provenance information

    The software genrates provenance information of results following accepted standards (PROV) 

    | Why should we measure it?  | How do we measure it? | Types it applies to  |
    |----------------------------|-----------------------|----------------------|
    | Provenance information is a key element of FAIR data.  Ideally, FAIR software should produce FAIR Data, of which provenance is a very important part.| Not measured. | all |
   

