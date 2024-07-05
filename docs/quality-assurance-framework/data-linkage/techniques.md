# Data linkage techniques

## Probabilistic linkage

[Probabilistic record linkage](https://www.robinlinacre.com/probabilistic_linkage) is a method of linking records that do not have unique identifiers. It works by assigning a score to each pair of records, based on the likelihood that they belong to the same person, record or entity. The higher the score, the more likely the records truly match.

The score is calculated using a variety of factors, including the matching of names, dates of birth, and other identifying information. The more these factors match, the higher the score. It allows to find true matches despite the imperfection in identifiers.

A popular probabilistic linkage approach is the [Fellegi and Sunter](https://courses.cs.washington.edu/courses/cse590q/04au/papers/Felligi69.pdf) model which has set the foundation for other implementations like [Splink](https://github.com/moj-analytical-services/splink) and [FastLink](https://imai.fas.harvard.edu/research/files/linkage.pdf). This framework is based on a Naïve Bayes approach, which uses likelihood ratios to calculate the probability of agreement on each matching variable.

## Deterministic linkage

[Deterministic record linkage](https://www.gov.uk/government/publications/joined-up-data-in-government-the-future-of-data-linking-methods/quality-assessment-in-data-linkage#references) is a simpler method of linking records. It works by using a set of rules to determine whether two records belong to the same entity (person, event, location). The rules typically involve combinations of identifiers, such as date of birth, postcode, and others.

More complex deterministic methods may incorporate the use of partial identifiers, phonetic codes, or transposition of elements. These methods, along with similarity scores, or distance-based measures (like Mahalanobis distances), can also be incorporated into deterministic linkage rules.

Deterministic algorithms typically fail to identify matches in scenarios with low data quality. The match does not need to be perfect. If the rules establish that partial-matches are accepted, then you can have a non-perfect match.

Deterministic algorithms may be overly conservative in identifying matches, leading to large numbers of missed matches which will then risk creating duplicate personas.

## Hybrid linkage

A [hybrid approach](https://pubmed.ncbi.nlm.nih.gov/32049329/) to record linkage using a combination of deterministic and probabilistic methodology has been seen to result in increased linkage accuracy and identified pairs of linked record that would have otherwise been missed when using any independent linkage technique.

## Machine learning based linkage

There are alternative methods for data linkage that use machine learning. Supervised techniques use classification methods to find pairs of records while others used clustering. It has been observed that machine learning methods can achieve higher quality in linkage when sufficient training data is available, but there is a lack of large-scale comparisons in the literature. [This](https://github.com/djvanderlaan/reclin2) is an example of a package for data linkage using ML. Using random forest, a decision-tree based model, [this](https://ijpds.org/article/view/1571#:~:text=Clerical%20review%20in%20probabilistic%20data,to%20find%20similarity%20for%20matching.) study managed to obtain an accuracy of 98% which does not seem too impressive in comparison with other methods.

Linking databases is not always possible due to the sensitive nature of the data. Organisations often cannot share their sensitive data due to privacy and confidentiality concerns, which makes it difficult to build models for record linkage across multiple organizations' databases. There are methods using deep learning that can preserve the privacy or the records ([see this study](https://arxiv.org/abs/2211.02161)). The approach involves each database owner training a local deep learning model. These models are then uploaded to a secure environment and aggregated to create a global model. The global model is used by a linkage unit to determine whether unlabelled record pairs are matches or non-matches.

!!! abstract "Good reads"

    - Simulation study: [When to conduct probabilistic linkage vs. deterministic linkage?](https://www.sciencedirect.com/science/article/pii/S1532046415000921)

    - Methodology report: [Methods for Automatic record matching and linkage and their use in National Statistics](https://s3.amazonaws.com/escoe-website/wp-content/uploads/2019/11/21120237/GSS-Methodology-Series-No.-25-Methods-for-automatic-record-matching-and-linkage-and-their-use-in-national-statistics.pdf)

    - Full report (Annex A1): [Enabling Data Linkage to Maximise the Value of Public Health Research Data](https://cms.wellcome.org/sites/default/files/enabling-data-linkage-to-maximise-value-of-public-health-research-data-phrdf-mar15.pdf)
