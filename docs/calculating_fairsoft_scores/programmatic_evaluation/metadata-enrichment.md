# Metadata enrichment

Metadata extracted automatically or provided manually is often incomplete for FAIRsoft evaluation. Enrichment helps produce more informative results and more useful feedback.


!!! note "When enrichment is useful"

    You may want to enrich metadata when:

    - important fields are missing
    - some fields are present but too generic
    - metadata needs to reflect additional documentation, publications, formats, or dependencies
    - you want a more informative FAIRsoft assessment


## Common fields to enrich

Typical metadata fields include:

- software type
- dependencies
- supported operating systems
- input and output formats
- documentation links
- publications
- download links

## Example

A minimal metadata object:

```json
{
  "name": "Flower",
  "type": "lib",
  "repository": [
    "https://github.com/adap/flower"
  ],
  "version_control": true
}
```

can be enriched with additional information such as: 

```json
{
  "name": "Flower",
  "type": ["lib"],
  "repository": [
    "https://github.com/adap/flower"
  ],
  "webpage": [
    "https://flower.ai"
  ],
  "version_control": true,
  "license": [
    {
      "name": "Apache License 2.0",
      "url": "https://opensource.org/licenses/Apache-2.0"
    }
  ],
  "documentation": [
    {
      "type": "readme",
      "url": "https://github.com/adap/flower/blob/main/README.md"
    }
  ],
  "input": [
    {
      "term": "CSV",
      "vocabulary": "EDAM"
    }
  ],
  "output": [
    {
      "term": "model",
      "vocabulary": "EDAM"
    }
  ]
}
``` 

## Related pages 

- See [Accepted metadata structure](accepted-metadata-structure.md)￼ for the expected metadata format
- See [Evaluate existing metadata](./existing/quickstart.md)￼ to send metadata directly for FAIRsoft evaluation
- See [GitHub full workflow](./github/quickstart.md)￼ to enrich metadata extracted from repositories