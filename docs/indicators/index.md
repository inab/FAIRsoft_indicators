
# Indicators Structure 

The collection of FAIRsoft indicators consists of **high-level** and **low-level** indicators that are designed to evaluate the FAIRness of research software. 


## High-level Indicators 

High-level indicators are broad criteria that capture the essential aspects of FAIRness in research software. These indicators are based on the FAIR principles and provide a comprehensive overview of the software's adherence to these principles. 

The high-level indicators are denoted by a letter and a number, where the letter represents the FAIR principle and the number represents the indicator within that principle. For example, F3 represents the third indicator under the Findability principle.

!!! example "Examples of High-level Indicators"

    - F3: Discoverability
    - I1: Data Format Standards and Practices
    - R1: Usage Documentation

## Low-level Indicators

Low-level indicators are specific criteria that support the high-level indicators by providing detailed guidance on how to assess the FAIRness of research software. These indicators are more granular and actionable, allowing developers and stakeholders to evaluate the software's compliance with the FAIR principles in a more detailed and systematic manner. 

Low-level indicators are denoted by a letter, a number, and a sub-number, where the letter represents the high-level indicator, the number represents the low-level indicator within that high-level indicator, and the sub-number represents the sub-indicator within the low-level indicator. For example, F3.1 represents the first low-level indicator under the third high-level indicator of the Findability principle.

!!! example "Examples of Low-level Indicators"
    F3 (Discoverability) has the following low-level indicators: 

    - F3.1: Discoverability in software registries
    - F3.2: Discoverability in software repositories
    - F3.3: Discoverability in literature

## Applicability 

Not all indicators apply to all types of software. Some indicators may be more relevant to certain types of software than others, depending on the nature of the software and its intended use.The FAIRsoft indicators assume two main types of software: "web" and "non-web" software. "Web" software refers to software that is accessed through the web, such as web applications, online tools, and APIs. "Non-web" software refers to software that is installed and run locally on a user's machine, such as desktop applications, command-line tools, and libraries. 

The applicability of each indicator is indicated in the indicator description. 

!!! example "Examples of applicability of indicators"
    - A1.1. Existence of an API or Web Interface
        - Applicability: Web
    - A1.2. Existance of downloadable and buildable software working version
        - Applicability: Non-web
    - I1.1. Use of standard data formats
        - Applicability: All


## Scores and Scoring Method

The indicators can be scored based on the software's compliance with the indicator criteria, with higher scores indicating a higher level of FAIRness. 

The scores range from 0 to 1, with 1 being the highest possible score. Each indicator has a different weight that contributes to the total score. The weights reflect the relative importance of each indicator in assessing the overall FAIRness of the software.

Both low-level indicators and high-level indicators have weights. These weights determine the impact of each indicator on the overall score. The weights can be adjusted based on the specific requirements and priorities of the software evaluation process.


!!! info "Why scores?"

    Scores allow us to calculate statistics and analyze the overall FAIRness of collections of software or individual tools. These statistics help developers and stakeholders identify areas for improvement and make informed decisions about the software's FAIRness.  

    However, scores should be understood as a general indication of the software's FAIRness, rather than a definitive assessment. Since the indicators they are based on may not capture all aspects of FAIRness, it is important to consider the scores in conjunction with other information about the software, such as its intended use, user community, and development context.
    
    
## Overview of Indicators 

The following figure provides an overview of the high-level indicators and their relationships to the FAIR principles. The figure illustrates how the high-level indicators are organized under each principle and how they contribute to the overall assessment of the software's FAIRness. 

!!! tip "Key Points" 
    - The weights of the high-level indicators are indicated in a rectanguler tag in the arrow that contects the indiator to the principle. As explained before, the weights are used to calculate the overall score of the software based on its compliance with the indicators. 
    - The weights of the low-level indicators are not shown in the figure, but they are used to calculate the score of the high-level indicators to which they belong. These weights are specified in the respective sections of the indicators, along with a detailed explanation of the rationale for measuring the indicator, the method of measurement, and the types of software to which it applies. 
    - Indicators that are not yet implemented are shown in gray. 
    - Not all indicators apply to all types of software. See the legend of the figure for more information on the applicability of each indicator.


![Figure](images/Fig1.svg){: width="105%"}
