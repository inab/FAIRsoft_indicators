
# Evaluate existing metadata

!!! info ""
    This workflow is for users who already have software metadata and want to compute **FAIRsoft indicators** directly, without going through GitHub metadata extraction.


## Evaluation workflow

```
Existing metadata
      ↓
(Optional) metadata enrichment
      ↓
FAIRsoft evaluation
      ↓
Scores, logs and feedback
```

In this workflow, metadata is sent directly to the **[Software Observatory evaluation API](https://observatory.openebench.bsc.es/api/docs)**.

---

## API endpoint

Send a `POST` request to:

```
https://observatory.openebench.bsc.es/api/fair/evaluate
```

The request body must contain a `tool_metadata` object.

---

## Minimal request

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

This is enough to run the evaluation, although the resulting FAIRsoft scores will depend strongly on the amount of metadata provided.

!!! note
    Minimal metadata allows the evaluation to run, but richer metadata leads to more informative FAIRsoft results.

---

## Minimal Python example

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

## Richer request example

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

## Response structure

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

## Accepted metadata structure

The `tool_metadata` object follows the metadata model expected by the evaluation API.

### Commonly used fields

| Field | Type | Notes |
|------|------|------|
| `name` | string | Software name |
| `type` | string or list of strings | Will be coerced to a list internally |
| `version` | string or list of strings | Will be coerced to a list internally |
| `description` | list of strings | Free-text descriptions |
| `label` | list of strings | Alternative names or labels |
| `repository` | list of URLs | Source code repositories |
| `webpage` | list of URLs | Project websites or API base URLs |
| `download` | list of URLs | Download locations |
| `src` | list of URLs | Source code links |
| `license` | list of objects | See License structure below |
| `documentation` | list of objects | See Documentation structure below |
| `authors` | list of objects | See Person structure below |
| `publication` | list of objects | See Publication structure below |
| `dependencies` | list of strings | Declared dependencies |
| `input` / `output` | list of objects | Controlled terms or formats |
| `topics` / `operations` | list of objects | Controlled terms |
| `os` | list of strings | Supported operating systems |
| `version_control` | boolean | Whether version control is used |
| `registration_not_mandatory` | boolean | Whether registration is not required |
| `registries` | list of strings | Known software registries |
| `e_infrastructures` | list | Referenced e-infrastructures |

### Nested object examples

**License**

```json
{
  "name": "Apache License 2.0",
  "url": "https://opensource.org/licenses/Apache-2.0"
}
```

**Documentation**

```json
{
  "type": "readme",
  "url": "https://github.com/adap/flower/blob/main/README.md"
}
```

**Person**

```json
{
  "name": "Jane Doe",
  "type": "person",
  "email": "jane@example.org",
  "maintainer": true
}
```

**Publication**

```json
{
  "title": "Example software paper",
  "year": 2023,
  "doi": "10.1234/example"
}
```

**Controlled term**

Used for fields such as `topics`, `operations`, `input`, and `output`.

```json
{
  "term": "CSV",
  "vocabulary": "EDAM",
  "uri": "http://edamontology.org/format_3752"
}
``` 

??? info "JSON schema"
    The full JSON schema for `tool_metadata` is available in the API documentation.


### Notes on accepted values

A few model behaviors are useful to know:

- `type` may be provided as a single string or a list of strings
- `version` may be provided as a single string or a list of strings
- empty strings in some optional fields are filtered out
- many fields are optional, but missing metadata will reduce the informativeness of the evaluation

!!! note
    If you only need a simple evaluation, a minimal object with `name`, `type`, and `repository` is often enough to get started.

