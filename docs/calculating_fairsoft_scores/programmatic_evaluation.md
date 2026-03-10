# Programmatic evaluation 

This tutorial explains how to compute FAIRsoft indicators programmatically for one or more GitHub repositories using the Software Observatory APIs.

Programmatic evaluation is useful when you want to:  

- evaluate multiple repositories
- perform benchmarking or review studies
- integrate FAIRsoft scoring into data analysis workflows
- inspect indicator logs and metadata coverage

## Evaluation workflow 

The programmatic evaluation process follows these steps:

```
GitHub repository
      ↓
Metadata extraction
      ↓
(Optional) metadata enrichment
      ↓
FAIRsoft evaluation
      ↓
Scores and evaluation logs
```

Two APIs are involved: 

| API | Purpose |
|-----|---------|
|GitHub metadata API | Extract structured metadata from repositories |
| Software Observatory API| Compute FAIRsoft indicators | 


!!! warning
The GitHub Metadata API is not the official GitHub REST or GraphQL API.
It is a higher-level API built on top of GitHub APIs and repository content inspection in order to extract as much FAIR-relevant metadata as possible from a repository. 


## Quickstart 

The following minimal script computes FAIRsoft scores for several GitHub repositories.

### Requirements 

Install the required Python packages:  

```sh
pip install requests pandas
```

You will also need a **GitHub personal access token**. 


### Example evaluation script 

```python
import requests
import pandas as pd

token = "YOUR_GITHUB_TOKEN"

repositories = {
    "Substra": "https://github.com/Substra/substrafl",
    "Flower": "https://github.com/adap/flower",
    "Vantage6": "https://github.com/vantage6/vantage6",
}

GITHUB_METADATA_API = "https://observatory.openebench.bsc.es/github-metadata-api/metadata/user"
OBSERVATORY_API = "https://observatory.openebench.bsc.es/api/fair/evaluate"


def get_repository_metadata(owner, repo):

    payload = {
        "owner": owner,
        "repo": repo,
        "userToken": token,
        "prepare": False
    }

    r = requests.post(GITHUB_METADATA_API, json=payload)
    r.raise_for_status()

    return r.json()["data"]


def compute_fairsoft(metadata):

    r = requests.post(
        OBSERVATORY_API,
        json={"tool_metadata": metadata, "prepare": False}
    )

    r.raise_for_status()

    return r.json()


results = []

for tool, url in repositories.items():

    owner = url.split("/")[-2]
    repo = url.split("/")[-1]

    metadata = get_repository_metadata(owner, repo)

    # minimal metadata enrichment
    metadata["type"] = "lib"
    metadata["version_control"] = True

    evaluation = compute_fairsoft(metadata)

    result = evaluation["result"]

    results.append({
        "tool": tool,
        "F": result["F"],
        "A": result["A"],
        "I": result["I"],
        "R": result["R"]
    })


df = pd.DataFrame(results)

print(df)

```

Example output: 

```text
      tool      F      A      I      R
0   Substra   0.82   0.75   0.61   0.79
1   Flower    0.91   0.80   0.73   0.84
2   Vantage6  0.77   0.69   0.66   0.81
```

--- 

## Full workflow 

The following sections explain each step in more detail. 

###  Retrieve repository metadata

Metadata is extracted from GitHub using the [GitHub Metadata API](). 

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
This API builds Observatory-compatible metadata by querying GitHub and inspecting repository contents.

??? info "Metadata extraction under the hood"

    The GitHub Metadata API extracts information such as:
        •	repository name and description
        •	homepage and repository URLs
        •	releases and version tags
        •	license information
        •	authors inferred from commit history
        •	repository topics
        •	publication information
        •	documentation files and their types
        •	citation metadata from CITATION.cff

    In practice, the API combines information from:
        •	the GitHub GraphQL API
        •	the repository root contents
        •	common documentation folders such as docs/, documentation/, and example/
        •	files such as:
        •	README
        •	CONTRIBUTING
        •	LICENSE
        •	CHANGELOG
        •	INSTALL
        •	USAGE
        •	API
        •	FAQ
        •	TUTORIAL
        •	REQUIREMENTS
        •	CITATION.cff

    It also tries to extract publication metadata from CITATION.cff and BibTeX-like content when available.



!!! note
The GitHub Metadata API provides a useful starting point, but the resulting metadata is often incomplete for FAIRsoft evaluation. Manual enrichment is usually needed for the best results.


## 2. Clean the data 

Some fields may require small adjustments before evaluation. 

### Removing placeholder GitHub emails 

```python
def manage_authors(metadata):

    if "authors" not in metadata:
        return metadata

    metadata["authors"] = [
        a for a in metadata["authors"]
        if not a.get("email", "").endswith("@users.noreply.github.com")
    ]

    return metadata
``` 

### 3. Add missing metadata 

GitHub metadata alone is often not sufficient for a meaningful FAIRsoft evaluation. 

Some information may need to be added manually. 

```python
metadata["type"] = "lib"
metadata["webpage"] = ["https://flower.ai"]
metadata["version_control"] = True
``` 

Allowed values for type include:  

```
cmd # comand-line
web # web application
db # database
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

Adding missing metadata improves the accuracy of FAIRsoft indicators.

### 4. Compute FAIRsoft indicators 

Send the metadata to the [Software Observatory evaluation API](). 

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

The response contains: 

- computed FAIRsoft indicators
- evaluation logs explaining how they were derived
- feedbach from the evaluator as "strenghts" and "how to improve" 

## Understanding the results 

The evaluation response contains three main components. 

### Result

The `result` field contains the computed FAIRsoft scores and lower-level indicators

Example fields include: 

- F, A, I, R: the four main FAIRsoft dimensions
- F1, F2, F3, A1, I1, R2, etc.: principle-level indicators
- F1_1, F1_2, A1_3, etc.: lower-level checks used to compute the indicators
- basic metadata fields such as name, type, and version 

For example: 
- F = 0.8 means the software scores well overall on Findability
- R = 0.8 means it also performs well overall on Reusability
- lower-level booleans such as F1_1 = `true` indicate whether specific checks passed

You will often use F, A, I, and R for comparisons, while the lower-level indicators are useful for deeper inspection.

### Logs 

The `logs` field provides explanations for each indicator.

The value is a list of messages describing: 
- what was checked
- which metadata fields were inspected
- why the indicator passed or failed
- whether the indicator was not applicable or not currently measured


This information is useful for:
- debugging evaluations
- understanding low scores
- identifying missing metadata 


### Feedback

The feedback field provides short human-readable guidance for each FAIR principle (F, A, I, R).

For each principle, it includes: 

- `strengths`: positive aspects already supported by the metadata
- i`mprovements`: concrete suggestions to improve the score

For example, feedback may suggest:

- registering the tool in software registries
- adding standard ontologies
- improving installation instructions
- declaring dependencies
- exposing a library or API
- adding release and contribution policies

This field is especially useful when the tutorial is used not only for scoring, but also for identifying actionable improvements.

## Tips

!!! warning
    FAIRsoft scores depend strongly on the available metadata.
    Low scores do not necessarily reflect poor software practices — they may indicate incomplete metadata.

!!! tip
    For large repository sets, start with a fully automated evaluation and then enrich metadata selectively.

!!! tip
    For single tools where metadata needs manual completion, consider using the FAIRsoft Evaluator instead of the programmatic workflow. 


## Related resources

- [GitHub Metadata API](ttps://observatory.openebench.bsc.es/github-metadata-api/api-docs/) 
- [Software Observatory API](https://observatory.openebench.bsc.es/docs/api/)
- [FAIRsoft Evaluator](https://openebench.bsc.es/observatory/Evaluation)
