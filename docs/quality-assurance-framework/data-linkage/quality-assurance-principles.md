# Data linkage quality assurance principles

## Linkage quality

Linkage quality refers to the accuracy and reliability of the data linkage process. The goal is to minimize linkage errors, ensuring that matched records truly belong to the same entity while avoiding false positives and negatives.

Several factors impact linkage quality, the data quality of the inputs and the data linkage technique. It is essential to address the issues found during the data preparation stage or at least account for those when analysing the linked asset.

Maximizing linkage rates is important but should not be over-optimized, as it may compromise the accuracy of the matches.

Another important aspect of the quality of the linkage is the processing speed. It is determined by the average computational time required to perform matches with different dataset sizes. Faster data linkage processes can lead to cost savings and improved efficiency but specially in the health and care world, this should not be made a priority. Key factors affecting data linkage include:

- **The choice of algorithms:** Deterministic algorithms typically have shorter computation times than probabilistic algorithms, but they may compromise linkage quality.

- **The size of datasets being linked:** Larger datasets may require more computational resources and lead to longer processing times.

## Transparency

It is critical for data linkage users to have confidence in the results and to understand the strengths and limitations of the methods used. There are several ways to ensure transparency in data linkage:

- Providing users with access to link confidence scores, enabling them to perform sensitivity analysis.

- Clearly documenting the methods used for data linkage, including strengths, limitations, and potential impacts on specific use cases.

- Offering both non-technical and technical documentation, such as user manuals explaining how to interpret the outputs, and detailed explanations of the methods used. A good example of this can be seen on the Master Person Service’ [Person_ID handbook for HES users](https://digital.nhs.uk/binaries/content/assets/website-assets/services/mps/the-person_id-handbook-for-hes-users-v1.0.4.pdf).

## Scalability
