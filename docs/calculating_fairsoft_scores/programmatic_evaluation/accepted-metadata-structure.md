# Accepted metadata structure

The `tool_metadata` object follows the metadata model expected by the FAIRsoft evaluation API.

Many fields are optional, but richer metadata generally leads to more informative FAIRsoft results.

## Top-level structure

The request body sent to the evaluation API must contain a `tool_metadata` object:

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

## Commonly used fields

| Field | Type | Notes |
|------|------|------|
| `id` | string | Optional internal identifier |
| `name` | string | Software name |
| `type` | string or list of strings | A single string is accepted and converted internally to a list |
| `version` | string or list of strings | A single string is accepted and converted internally to a list |
| `authors` | list of `Person` objects | See object structure below |
| `bioschemas` | boolean | Whether Bioschemas metadata is available |
| `contribPolicy` | list of strings | Contribution policy information |
| `dependencies` | list of strings | Declared dependencies |
| `description` | list of strings | Free-text descriptions |
| `documentation` | list of `Documentation` objects | See object structure below |
| `download` | list of URLs | Download locations |
| `edam_operations` | list of URLs | EDAM operation URIs |
| `edam_topics` | list of URLs | EDAM topic URIs |
| `https` | boolean | Whether HTTPS is used |
| `input` | list of `ControlledTerm` objects | See object structure below |
| `inst_instr` | boolean | Whether installation instructions are available |
| `label` | list of strings | Alternative names or labels |
| `license` | list of `License` objects | See object structure below |
| `links` | list of URLs | Related links |
| `operational` | boolean | Whether the software is operational |
| `os` | list of strings | Supported operating systems |
| `output` | list of `ControlledTerm` objects | See object structure below |
| `publication` | list of `Publication` objects | See object structure below |
| `repository` | list of URLs | Source code repositories |
| `semantics` | object | Free-form semantic metadata |
| `source` | list of strings | Source descriptors |
| `src` | list of URLs | Source code locations |
| `ssl` | boolean | Whether SSL is used |
| `tags` | list of strings | Tags or keywords |
| `termsUse` | boolean | Whether terms of use are available |
| `test` | list | Free-form test-related information |
| `topics` | list of `ControlledTerm` objects | See object structure below |
| `operations` | list of `ControlledTerm` objects | See object structure below |
| `webpage` | list of URLs | Project websites or API base URLs |
| `registration_not_mandatory` | boolean | Whether registration is not required |
| `registries` | list of strings | Known software registries |
| `other_versions` | list of strings | Additional version labels |
| `e_infrastructures` | list | Referenced e-infrastructures |
| `version_control` | boolean | Whether version control is used |

## Minimal example

A minimal metadata object may look like this:

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

## Nested object structures

### License object

Used in the `license` field.

| Field | Type | Required | Notes |
|------|------|----------|------|
| `name` | string | Yes | License name |
| `url` | URL | No | License URL; empty strings are accepted and converted to null |

Example:

```json
{
  "name": "Apache License 2.0",
  "url": "https://opensource.org/licenses/Apache-2.0"
}
```

### Documentation object

Used in the `documentation` field.

| Field | Type | Required | Notes |
|------|------|----------|------|
| `type` | string | Yes | Documentation type, for example `readme` |
| `url` | URL | No | URL of the documentation resource |

Example:

```json
{
  "type": "readme",
  "url": "https://github.com/adap/flower/blob/main/README.md"
}
```

### Person object

Used in the `authors` field.

| Field | Type | Required | Notes |
|------|------|----------|------|
| `name` | string | Yes | Person name |
| `type` | string | Yes | Usually `person` |
| `email` | string | No | Email address; empty strings are accepted and converted to null |
| `maintainer` | boolean | No | Defaults to `false` |

Example:

```json
{
  "name": "Jane Doe",
  "type": "person",
  "email": "jane@example.org",
  "maintainer": true
}
```

### Publication object

Used in the `publication` field.

| Field | Type | Required | Notes |
|------|------|----------|------|
| `doi` | string | No | DOI identifier |
| `pmcid` | string | No | PubMed Central identifier |
| `pmid` | string | No | PubMed identifier |
| `cit_count` | integer | No | Citation count |
| `ref_count` | integer | No | Reference count |
| `refs` | list of objects | No | Free-form reference metadata |
| `title` | string | No | Publication title |
| `year` | integer | No | Publication year; strings are converted to integers |
| `citations` | list of objects | No | Free-form citation metadata |

Example:

```json
{
  "title": "Example software paper",
  "year": 2023,
  "doi": "10.1234/example"
}
```

### Controlled term object

Used in the `topics`, `operations`, `input`, and `output` fields.

| Field | Type | Required | Notes |
|------|------|----------|------|
| `vocabulary` | string | No | Vocabulary name, for example `EDAM` |
| `term` | string | No | Human-readable term |
| `uri` | URL | No | Term URI |

Example:

```json
{
  "term": "CSV",
  "vocabulary": "EDAM",
  "uri": "http://edamontology.org/format_3752"
}
```

## URL fields

The following fields expect URLs:

- `repository`
- `webpage`
- `download`
- `src`
- `links`
- `edam_topics`
- `edam_operations`
- `license[].url`
- `documentation[].url`
- `topics[].uri`
- `operations[].uri`
- `input[].uri`
- `output[].uri`

## Notes on accepted values

A few model behaviors are useful to know:

- `type` may be provided as a single string or a list of strings
- `version` may be provided as a single string or a list of strings
- empty strings in some optional fields are filtered out or converted to null
- empty entries in `publication` are removed before validation
- many fields are optional, but missing metadata will reduce the informativeness of the evaluation

!!! note
    If you only need a simple evaluation, a minimal object with `name`, `type`, and `repository` is often enough to get started.

??? info "JSON schema"
    The full JSON schema for the request body is available [here](https://github.com/inab/observatory-api/blob/main/metadata_request.schema.json).
