---
hide:
  - navigation
---

# Implementation

## Techniques and Tools

The selection of tools and techniques for Data Linkage must be documented and justified to suit the specific application.

!!! info "Type: Process"

    === "Recommendations"

        Some examples of options are

        - Matching methods: deterministic, probabilistic, hybrid or machine learning-based matching.

        - Tools: publicly available libraries (e.g. Splink), internal off-the shelf services (e.g. MPS), third-party proprietary software (AWS Glue).


        The selection of tools and techniques is influenced by various factors. Employ the Triage guidelines to ensure comprehensive consideration of all relevant factors when choosing the appropriate tools and techniques.

        When employing an existing model, justify this decision and clearly specify the version being used. Explain why it aligns with your case and data requirements.


    === "RAG"
    
        &#128308; **RED:** <br>
        Inappropriate or inconsistent use of linkage techniques that are not aligned with the nature and quality of the data, resulting in inaccurate or unreliable linkages. There is a reliance on methodologies and tools that are unsuitable or not fit for purpose, leading to suboptimal results.

        &#128993; **AMBER:** <br>
        Some consideration given to the nature and quality of the data when selecting linkage techniques, but there may still be instances where inappropriate methodologies and tools are used, leading to room for improvement in the applicability or efficiency of the linkages.

        &#128994; **GREEN:** <br>
        Careful consideration of the nature and quality of the data to select appropriate linkage techniques. State-of-the-art methodologies and tools are employed, including deterministic matching for exact matches and probabilistic matching for likely matches. There is a focus on the efficient and accurate delivery of results, without relying on unsuitable methodologies or tools.

## Configuration of linkage parameters/settings

Data Linkage models depend on parameters such as: the choice of blocking variables, matching thresholds, weight assignments for different linkage features, etc.

The quality assurance of linkage parameters involves different requirements if the data linker sets up a bespoke model (A) or use an established model (B).

!!! info "Type: Data"

    === "Recommendations"

        Option (A) - Bespoke model

        - Fine-tune parameters: Adjust settings like matching thresholds and weights based on your data quality and business case.

        - Data-driven decisions: Test different configurations to optimise accuracy and reliability, and document final choices for transparency.

        - Version control: Share and store parameter settings for future reference.

        Option (B) - Established model

        - Understand your parameters: Evaluate what is built-in to the model and their impact on results.

        - Documentation: Rely on existing model documentation to assess settings.

        - Investigate data interaction: Test and document how the model's parameters interact with your specific data.


        Employ the Triage guidelines to ensure comprehensive consideration of all relevant factors when choosing the appropriate parameters and settings.



    === "RAG"

        **Option (A) - Bespoke model**

        &#128308; **RED:** <br>
        Linkage parameters are inadequately configured leading to inaccurate or unreliable linkages. No consideration for data quality or business needs.

        &#128993; **AMBER:** <br>
        Some parameter consideration, but inconsistent. Iteration lacks systematic approach.

        &#128994; **GREEN:** <br>
        Linkage parameters are carefully configured based on data quality and specific business needs. Adjustment is made when necessary to enhance accuracy and reliability. Iterative refinement is systematic, informed by evaluation and quality assessment.

        **Option (B) - Established model**

        &#128308; **RED:** <br>
        Data linker is unaware of the parameters involved in the established model, and has not carried out an impact assessment on the data in hand.

        &#128993; **AMBER:** <br>
        Data linker is aware of the parameters involved in the established model, but has not carried out an impact assessment on the data in hand.

        &#128994; **GREEN:** <br>
        Data linker is aware of the parameters involved in the established model, and has carried out an impact assessment on the data in hand.

## Version control

Version control guarantees consistent, traceable, and reproducible outcomes for the data linkage process.

!!! info "Type: Process"

    === "Recommendations"

        - Code: Track changes to the main linkage process code for easy debugging and updates.
        - Libraries: Monitor any external code used.
        - Model Parameters: Record adjustments to settings for transparency and optimisation.
        - Analyses: Preserve profiling and test outcomes for future comparison, enhancement, and methodology validation.
        - Assessment Card:  Monitor the evolution of your linkage methodology and its performance.

    === "RAG"

        &#128308; **RED:** <br>
        Absence of a version control process in the data linkage procedure.

        &#128993; **AMBER:** <br>
        Basic version control process is in place but lacks comprehensive tracking and management features.

        &#128994; **GREEN:** <br>
        Robust version control system is in place, effectively tracking changes and managing different versions throughout the data linkage process.


If you have any ideas or feedback you'd like to give the team, feel free to [contact us](<https://github.com/nhsengland/quality-assurance-framework-for-data-linkage/issues/new?assignees=&labels=&projects=&template=send-feedback-on-the-quality-assurance-framework-for-data-linkage.md&title=>)