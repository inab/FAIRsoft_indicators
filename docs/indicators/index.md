# Indicators Structure

Welcome to the comprehensive guide on FAIRsoft indicators, designed to systematically assess the FAIRness of research software. Our indicators are split into two categories: high-level and low-level, each tailored to provide insights at different granularity levels.

## High-level Indicators

High-level indicators represent overarching aspects of FAIRness based on the FAIR principles, offering a broad evaluation of software adherence to these principles. These indicators are categorized by the specific FAIR principle they assess:

- **F (Findability)**
- **A (Accessibility)**
- **I (Interoperability)**
- **R (Reusability)**

Each indicator is denoted by a letter representing the principle followed by a number indicating its position within that category, e.g., F3 for the third Findability indicator.

### Examples of High-level Indicators

- **F3: Discoverability** - Assessing the ease with which software can be found by both humans and machines.
- **I1: Data Format Standards and Practices** - Evaluating adherence to industry standards in data formatting.
- **R1: Usage Documentation** - Examining the availability and comprehensiveness of documentation.

## Low-level Indicators

Low-level indicators provide detailed, actionable criteria supporting the high-level indicators. These indicators delve deeper into specific aspects of FAIRness, enabling a thorough assessment process.

Each low-level indicator is denoted by extending the high-level code with a sub-number, indicating its detailed focus under the broader category, e.g., F3.1 for the first detailed aspect under the third Findability indicator.

### Examples of Low-level Indicators

- **F3.1: Discoverability in Software Registries**
- **F3.2: Discoverability in Software Repositories**
- **F3.3: Discoverability in Literature**

## Applicability

The relevance of each indicator may vary depending on the software type—whether it's "web" or "non-web":
- **Web software**: Applications accessed through the web, such as online tools and APIs.
- **Non-web software**: Applications run locally, like desktop apps and command-line tools.

### Examples of Applicability
- **A1.1: Existence of an API or Web Interface** - Applicable to Web.
- **A1.2: Existence of Downloadable and Buildable Software Version** - Applicable to Non-web.
- **I1.1: Use of Standard Data Formats** - Applicable to All.

## Scores and Scoring Method

Indicators are scored on a scale from 0 to 1, with 1 representing optimal FAIRness. Each indicator's weight influences the overall FAIRness score, highlighting its importance in the comprehensive assessment.

### Scoring Insights
Scores are instrumental in generating statistics that help evaluate the collective FAIRness of software portfolios, guiding improvements and strategic decision-making. Scores should be understood as a general indication of the software's FAIRness, rather than a definitive assessment

## Overview of Indicators

The indicators are visualized in a structured diagram that illustrates the connection between high-level indicators and the underlying FAIR principles. The diagram also highlights the weights assigned to each indicator, underscoring their significance in the overall evaluation process.

### Key Points in the Overview Diagram
- **Indicator Weights**: Displayed on the connecting arrows in the diagram, influencing the total FAIRness score. The weights of the low-level indicators are not shown in the diagram.
- **Implementation Status**: Unimplemented indicators are shown in gray to indicate their development status.
- **Software Type Applicability**: Not all indicators apply universally; specific applicabilities are noted in the diagram legend.

![Overview of FAIRsoft Indicators](images/Fig1.svg){: width="100%"}
