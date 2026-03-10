# Quickstart

!!! info
    This quickstart shows how to compute **FAIRsoft scores for multiple software tools** starting from existing metadata.

??? info "Jupyter notebook"
    Download the jupyter notebook of this quickstart [here](https://github.com/inab/FAIRsoft_indicators/blob/master/notebooks/existing-metadata-quickstart.ipynb)

## Requirements

Install the required Python packages:

```bash
pip install requests pandas
```

---

## Example script

```python
import requests
import pandas as pd

tools_metadata = {
    "Substra": {
        "name": "Substra",
        "type": "lib",
        "repository": ["https://github.com/Substra/substrafl"],
        "version_control": True
    },
    "Flower": {
        "name": "Flower",
        "type": "lib",
        "repository": ["https://github.com/adap/flower"],
        "version_control": True
    },
    "Vantage6": {
        "name": "Vantage6",
        "type": "lib",
        "repository": ["https://github.com/vantage6/vantage6"],
        "version_control": True
    }
}

OBSERVATORY_API = "https://observatory.openebench.bsc.es/api/fair/evaluate"


def compute_fairsoft(metadata):

    r = requests.post(
        OBSERVATORY_API,
        json={"tool_metadata": metadata, "prepare": False}
    )

    r.raise_for_status()

    return r.json()


results = []

for tool, metadata in tools_metadata.items():

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

### What the script does

1. Defines minimal software metadata for each tool
2. Sends the metadata to the FAIRsoft evaluation API
3. Collects the resulting FAIRsoft scores

### Next step

To learn more about the accepted input format and richer metadata objects, continue with:

- **[Accepted metadata structure](./accepted-metadata-structure.md)**
- **[Evaluate existing metadata](./existing-metadata.md)**