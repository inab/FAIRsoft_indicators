# Metadata enrichment

Metadata extracted automatically from GitHub is not complete enought to calculate all FAIRsoft indicators.

## Common fields to enrich

Typical metadata fields include:

- software type
- dependencies
- supported operating systems
- input and output formats
- documentation links
- publications
- download links

Example enrichment:

```python
metadata["type"] = "lib"
metadata["webpage"] = ["https://flower.ai"]
```


### Allowed values for type 

```
cmd       // command-line application
web       // web application
db        // database
app
lib
workflow
plugin
rest
sparql
suite
workbench
script
ontology
soap
``` 

