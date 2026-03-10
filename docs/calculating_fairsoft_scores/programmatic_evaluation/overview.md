# Programmatic evaluation

FAIRsoft indicators can be computed programmatically starting from either:

- one or more **GitHub repositories**
- **existing software metadata** that you already maintain elsewhere

Choose the workflow that best matches your starting point.

## Available workflows

### Evaluate GitHub repositories

Use this workflow when you want to start from one or more GitHub repository URLs.

Metadata is first extracted automatically from the repository, then optionally reviewed or enriched before computing FAIRsoft indicators.

→ **[Quickstart](github-quickstart.md)**: run a minimal script for one or more repositories  
→ **[Full workflow](github-workflow.md)**: learn the complete workflow, including metadata extraction, inspection, and enrichment

### Evaluate existing metadata

Use this workflow when you already have software metadata and want to send it directly for FAIRsoft evaluation.

→ **[Quickstart](quickstart.md)**: send a minimal metadata object and compute FAIRsoft indicators
→ **[Quickstart](existing-metadata-workflow.md)**: 

## Supporting guides

These pages provide reference material used across workflows:

- **[Accepted metadata structure](accepted-metadata-structure.md)**: expected structure of the `tool_metadata` object
- **[Metadata enrichment](metadata-enrichment.md)**: how to improve metadata before evaluation