
# Evaluate existing metadata

!!! info 
    
    This workflow is for users who already have software metadata and want to compute **FAIRsoft indicators** directly, without going through GitHub metadata extraction.


## Evaluation workflow

```
Existing metadata
      ↓
FAIRsoft evaluation
      ↓
Scores, logs and feedback
```

In this workflow, metadata is sent directly to the **[Software Observatory evaluation API](https://observatory.openebench.bsc.es/api/docs)**.

---


### API endpoint

Send a `POST` request to:

```
https://observatory.openebench.bsc.es/api/fair/evaluate
```

The request body must contain a `tool_metadata` object. 

For the  expected structure of this object, see:

→ [Accepted metadata structure](../accepted-metadata-structure.md)

---

### Minimal request

The following is the smallest useful request body for the evaluation API:

```json
{
  "tool_metadata": {
    "name": "Flower",
    "type": "lib",
    "repository": [
      "https://github.com/adap/flower"
    ],
    "version_control": true
  },
  "prepare": false
}
```


!!! note
    Minimal metadata allows the evaluation to run, but richer metadata leads to more informative FAIRsoft results.

---

### Minimal Python example

```python
import requests

OBSERVATORY_API = "https://observatory.openebench.bsc.es/api/fair/evaluate"

payload = {
    "tool_metadata": {
        "name": "Flower",
        "type": "lib",
        "repository": [
            "https://github.com/adap/flower"
        ],
        "version_control": True
    },
    "prepare": False
}

response = requests.post(OBSERVATORY_API, json=payload)
response.raise_for_status()

evaluation = response.json()
print(evaluation)
```

This example shows the essential pattern:

1. build a `tool_metadata` object
2. send it to the evaluation endpoint
3. read the returned evaluation

---

### Richer request example

A more complete metadata object may include fields such as `webpage`, `documentation`, `publication`, `license`, `dependencies`, `input`, or `output`.

```json
{
  "tool_metadata": {
    "name": "Flower",
    "type": ["lib"],
    "description": [
      "A framework for federated learning"
    ],
    "label": [
      "Flower"
    ],
    "repository": [
      "https://github.com/adap/flower"
    ],
    "webpage": [
      "https://flower.ai"
    ],
    "version": [
      "1.13.0"
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
    "authors": [
      {
        "name": "Jane Doe",
        "type": "person",
        "email": "jane@example.org",
        "maintainer": true
      }
    ],
    "publication": [
      {
        "title": "Flower: A Friendly Federated Learning Research Framework",
        "year": 2023,
        "doi": "10.48550/arXiv.2007.14390"
      }
    ],
    "topics": [
      {
        "term": "machine learning",
        "vocabulary": "EDAM"
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
  },
  "prepare": false
}
```

---

## Understanding the results

The API returns three main components:

- `result`
- `logs`
- `feedback`

### `result`

The `result` field contains:

- the main FAIRsoft scores: `F`, `A`, `I`, `R`
- principle-level indicators such as `F1`, `A1`, `I2`, `R3`
- lower-level checks such as `F1_1` or `I3_2`
- basic metadata fields such as `name`, `type`, and `version`

This is the main output used for comparisons or summaries.

### `logs`

The `logs` field explains how the indicators were computed.

It records:

- what was checked
- which metadata fields were used
- why a check passed or failed
- whether a check was not applicable or not currently measured

This is useful for debugging and interpretation.

### `feedback`

The `feedback` field provides human-readable suggestions for each FAIR principle.

For each of `F`, `A`, `I`, and `R`, it may include:

- `strengths`
- `improvements`

This is especially useful when the evaluation is used to guide metadata improvement.

---

## Next steps

- See [Accepted metadata structure](../accepted-metadata-structure.md)￼for the expected input format
- See [Metadata enrichment](../metadata-enrichment.md)￼for guidance on improving incomplete metadata



