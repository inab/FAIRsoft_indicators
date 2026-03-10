# Quickstart

!!! info
    This quickstart shows how to compute **FAIRsoft scores for multiple GitHub repositories** using the Software Observatory APIs.

??? info "Jupyter notebook"
    Download the jupyter notebook of this quickstart [here](https://github.com/inab/FAIRsoft_indicators/blob/master/notebooks/github-quickstart.ipynb)


## Requirements

Install the required Python packages:

```bash
pip install requests pandas
```

You will also need a **[GitHub personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#about-personal-access-tokens)** with read permisions for repositories.

--- 

## Example script 

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

```
      tool      F      A      I      R
0   Substra   0.82   0.75   0.61   0.79
1   Flower    0.91   0.80   0.73   0.84
2   Vantage6  0.77   0.69   0.66   0.81
```

### What the script does 

1.	Retrieves metadata from GitHub using the GitHub Metadata API
2.	Adds minimal required metadata
3.	Sends the metadata to the FAIRsoft evaluation API
4.	Collects the resulting FAIR scores


### Next step 

To better understand how the metadata extraction and evaluation work, continue with:

- **[Full workflow tutorial](./github-workflow.md)**

