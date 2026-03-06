# Programmatic evaluation

FAIRsoft indicators can be computed programmatically in different ways depending on your starting point.

### Evaluate GitHub repositories

If you start from GitHub repositories, metadata can be extracted automatically using the **GitHub Metadata API** before running the evaluation.

Available guides:

- [Quickstart tutorial](quickstart.md): run a minimal script to compute FAIRsoft scores for multiple repositories
- [GitHub repository workflow](workflow_a.md): learn the full workflow, including metadata extraction, inspection, and enrichment


!!! note "" 

    This is the best option if you want to:

    - evaluate repositories directly from GitHub
    - inspect and enrich extracted metadata


### Evaluate existing metadata

If you already have software metadata from another source, you can send it directly to the **Software Observatory evaluation API**. 

Available guide:

- [Existing metadata workflow](workflow_b.md)

!!! note ""

    This is the best option if you want to:

    - evaluate metadata you already maintain elsewhere
    - skip GitHub-based metadata extraction
    - integrate FAIRsoft evaluation into external metadata pipelines



---

## Available APIs

Two APIs are involved in these workflows:

| API | Purpose |
|-----|---------|
| **GitHub Metadata API** | Extract structured metadata from repositories |
| **Software Observatory API** | Compute FAIRsoft indicators |

!!! warning
    The **GitHub Metadata API** is not the official GitHub REST or GraphQL API.  
    It is a higher-level API built on top of GitHub APIs and repository content inspection in order to extract FAIR-relevant metadata from repositories.

---

## Related resources

- [GitHub Metadata API](https://observatory.openebench.bsc.es/github-metadata-api/api-docs/)
- [Software Observatory API](https://observatory.openebench.bsc.es/docs/api/)
- [FAIRsoft Evaluator](https://openebench.bsc.es/observatory/Evaluation)