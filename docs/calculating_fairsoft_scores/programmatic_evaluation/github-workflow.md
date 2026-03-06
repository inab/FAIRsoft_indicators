# Evaluate GitHub repositories

!!! info ""
    This tutorial explains each step involved in programmatic FAIRsoft evaluation given one or more GitHub repositories.


## 1. Retrieve repository metadata

Metadata is extracted from GitHub using the **[GitHub Metadata API](https://observatory.openebench.bsc.es/github-metadata-api/api-docs/)**.

```python
def get_repository_metadata(owner, repo):

    payload = {
        "owner": owner,
        "repo": repo,
        "userToken": token,
        "prepare": False
    }

    response = requests.post(GITHUB_METADATA_API, json=payload)
    response.raise_for_status()

    return response.json()["data"] 
``` 

??? note "Metadata extraction under the hood"
    The GitHub Metadata API extracts information such as:

    - repository name and description
    - homepage and repository URLs
    - releases and version tags
    - license information
    - authors inferred from commit history
    - repository topics
    - publication information
    - documentation files and their types
    - citation metadata from `CITATION.cff`

    The API combines data from:

    - the GitHub GraphQL API
    - repository contents
    - documentation directories such as `docs/` and `documentation/`
    - standard project files like `README`, `CONTRIBUTING`, `CHANGELOG`, and `CITATION.cff` 



## 2. Enrich metadata 

!!! info ""
    The extracted metadata is often incomplete for FAIRsoft evaluation and may require manual enrichment. 


Typical fields that may need enrichment include: `type`, `webpage`, `dependencies`, `input`, `output`, `os`, `publication`, `download` and `test`.

See the detailed guide on how to (manually) enrich metadata: 

→ [Metadata enrichment guide]()

## 3. Compute FAIRsoft indicators  

Once metadata is ready, it can be sent to the Software Observatory API.

```python
def compute_fairsoft(metadata):

    payload = {
        "tool_metadata": metadata,
        "prepare": False
    }

    response = requests.post(OBSERVATORY_API, json=payload)
    response.raise_for_status()

    return response.json()
```

The response contains: computed FAIRsoft indicators, evaluation logs and improvement suggestions.

## Understanding the results 

The evaluation response contains three main components: 

| Field | Description |
|-------|-------------|
| `result` | FAIRsoft scores and indicator values | 
| `logs` | Detailed explanation of each indicator| 
| `feedback` | Suggestions for improving FAIRness| 

### Result

The result field includes the four main FAIRsoft dimensions: 

```
F  Findability
A  Accessibility
I  Interoperability
R  Reusability
```

It also contains lower-level indicators such as: 

```
F1, F2, F3
A1, A2, A3
I1, I2, I3
R1, R2, R3
```

and detailed checks: 

```
F1_1
F1_2
A1_3
I3_1
```

### Logs

The logs field explains how each indicator was computed. Each entry describes: 

- what was checked
- which metadata fields were used 
- whether the check passed or failed and why

### Feedback

The feedback field provides human-readable improvement suggestions. For each FAIR principle it lists:

- `strengths`
- `improvements`