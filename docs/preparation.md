---
hide:
  - navigation
---

# Data preparation

## Profiling

Data profiling is the process of examining the data and collecting statistics and information about that data.
This is important for selecting the right blocking and matching variables and ensure accurate linkage results.

!!! info "Data Profiling"

    === "Recommendations"

        This includes establishing:

        - Data dictionary (data types, data meaning, etc)
        - Completeness (presence of missing or null values)
        - Uniqueness / cardinality (how many and which unique values a variable can have)
        - Validity of variable values (the values are included in the data dictionary, are valid, have a meaning)
        - Distribution of values / outliers
        - Basic statistics (min, max, mean, variance)
        - Correlations and functional dependencies between variables

    === "RAG"

        &#128308; **RED:** <br>
        No data profiling is performed before linking, leading to potential inconsistencies in the linked data.

        &#128993; **AMBER:** <br>
        Some data profiling is performed before linking, but it could be more thorough and systematic.

        &#128994; **GREEN:** <br>
        Comprehensive data profiling is performed before linking, identifying and resolving inconsistencies in datasets to be linked.

    === "Worked examples"
        ??? "Data Dictionary Creation"
            ```py exec="on" source="above" result="console" session="data_profiling"
            import pandas as pd

            input_data = [[1, 20240224, 'sample_name']]
            input_schema = ['id', 'dob', 'name']
            input_df = pd.DataFrame(input_data, columns = input_schema)

            def get_data_types(df):
                '''
                function to get data types of columns in a dataframe

                parameters:
                    df: Input DataFrame

                returns:
                    DataFrame: DataFrame with columns 'Column' and 'Data Type'
                '''

                data_types = [[col_name, str(col_type)] for col_name, col_type in zip(df.columns, df.dtypes)]

                schema =  ['Column', 'Data Type']

                result_df = pd.DataFrame(data_types, columns = schema)

                return result_df

            output = get_data_types(input_df)

            print(output)

            ```

        ??? "Completeness"
            ```py exec="on" source="above" result="console" session="datamaia.imaa_profiling"
            import pandas as pd

            input_data = [[1, 20240224, 'sample_name'], [None, 20240224, 'sample_name'],[1, 20240224, None], [1, 20240224, None]]
            input_schema = ['id', 'dob', 'name']
            input_df = pd.DataFrame(input_data, columns = input_schema)

            def null_percentage(df):
                '''
                Function to calculate the percentage of null values in each column of a pandas DataFrame.

                Parameters:
                    df (DataFrame): Input DataFrame

                Returns:
                    DataFrame: DataFrame with columns 'Column' and 'Null Percentage'
                '''

                total_rows = len(df)
                null_counts = df.isnull().sum()
                null_percentages = (null_counts / total_rows) * 100

                result_df = pd.DataFrame({'Column': null_percentages.index, 'Null Percentage': null_percentages.values})

                return result_df

            output = null_percentage(input_df)

            print(output)

            ```
        ??? "Uniqueness"
            ```py exec="on" source="above" result="console" session="datamaia.imaa_profiling"
            import pandas as pd

            input_data = [[1, 20240224, 'sample_name'], [None, 20240224, 'sample_name2'],[3, 20240224, None], [2, 20240224, None]]
            input_schema = ['id', 'dob', 'name']
            input_df = pd.DataFrame(input_data, columns = input_schema)

            def uniqueness(df):
                '''
                Function to calculate the uniqueness of values in each column of a pandas DataFrame.

                Parameters:
                    df (DataFrame): Input DataFrame

                Returns:
                    DataFrame: DataFrame with columns 'Column' and 'Uniqueness'
                '''
                unique_counts = df.nunique()
                total_rows = len(df)
                uniqueness_percentages = (unique_counts / total_rows) * 100

                result_df = pd.DataFrame({'Column': uniqueness_percentages.index, '# of Unique Values': unique_counts})

                return result_df

            output = uniqueness(input_df)

            print(output)

            ```
        ??? "Cardinality"
            ```py exec="on" source="above" result="console" session="datamaia.imaa_profiling"
            import pandas as pd

            input_data = [[1, 20240224, 'sample_name'], [None, 20240224, 'sample_name2'],[3, 20240224, 'sample_name2'], [2, 20240224, None]]
            input_schema = ['id', 'dob', 'name']
            input_df = pd.DataFrame(input_data, columns = input_schema)

            def cardinality(df, column_name):
                '''
                Function to calculate find what values a variable can have and how many times they appear each.

                Parameters:
                    df (DataFrame): Input DataFrame
                    column_name (str): name of the column that you want to know the cardinality of.

                Returns:
                    DataFrame: DataFrame with columns 'Value' and 'Count'
                '''
                value_counts = df[column_name].value_counts().reset_index()

                value_counts.columns = [column_name, 'count']

                return value_counts

            output = cardinality(input_df, 'name')

            print(output)

            ```
        ??? "Basic Stats"
            ```py title="Uniqueness" exec="on" source="above" result="console" session="data_uniqueness"
            import pandas as pd

            input_data = [[1, 'john', 23, 51], [2, 'lucy', 18, 103],[3,'claire', 55, 87], [4, 'sam', 44, 70]]
            input_schema = ['id', 'name','age', 'weight']
            input_df = pd.DataFrame(input_data, columns = input_schema)

            def basic_stats(df):
                '''
                Function to calculate the basic stats of values in each numerical column of a pandas DataFrame.

                Parameters:
                    df (DataFrame): Input DataFrame

                Returns:
                    DataFrame: DataFrame with columns 'Column', 'Mean', 'Median', 'Mode', 'Standard Deviation', 'Minimum', 'Maximum'
                '''
                numerical_columns = df.select_dtypes(include=['number']).columns.tolist()

                rows = []

                for column in numerical_columns:

                    mean = df[column].mean()
                    median = df[column].median()
                    std = df[column].std()
                    min = df[column].min()
                    max = df[column].max()

                    rows.append([column, mean, median, std, min, max])

                schema = ['column_name', 'mean', 'median', 'std', 'min', 'max']
                stats = pd.DataFrame(rows, columns = schema)

                return stats



            output = basic_stats(input_df)

            print(output)
            ```

## Assessment

Assessing the findings from data profiling means using that information to evaluate if the input data is fit for linkage purposes, and how the data profile affect the modelling choices for linkage.

!!! info "Data assessment"

    === "Recommendations"

        This includes (but it is not limited to):

        - Assessing if variables have inconsistent values across data sets, and how to address this issue
        - Deciding which variables are most suitable to be used as blocking variables and for distance calculations, considering completeness, quality and validity
        - Decide which variables to use if there are multiple variables carrying similar information (i.e. correlated)


    === "RAG"

        &#128308; **RED:** <br>
        Data profiling results have not been assessed. There has been no effort to evaluate the input data for its suitability for linkage purposes. There is no consideration given to the consistency of variables across datasets, the selection of suitable blocking variables, or the handling of correlated variables.

        &#128993; **AMBER:** <br>
        Some level of data assessment has been conducted, but it is incomplete or inconsistent. There may be efforts to evaluate certain aspects of the data, such as identifying inconsistent variable values or selecting blocking variables, but these assessments are not comprehensive.

        &#128994; **GREEN:** <br>
        A rigorous assessment was carried out. Findings are documented and inform subsequent decisions on the linkage methods.

    === "Worked examples"
        ??? "Profiling Assessment"
            ```py exec="on" result="console" session="data_profiling"
            import pandas as pd

            gender_cardinality_schema = ['gender', 'count']
            print("Table 1")
            data_table1 = [[1, 2238],[2, 1500],[9, 387],[0,100]]
            cardinality1 = pd.DataFrame(data_table1, columns = gender_cardinality_schema)
            print(cardinality1)
            print('\n')

            print("Table 2")
            data_table2 = [[1, 2555],[2, 3002],[0,233]]
            cardinality2 = pd.DataFrame(data_table2, columns = gender_cardinality_schema)
            print(cardinality2)
            ```
            In this case, table 1 that you are trying to link to table 2 has 4 possible values for gender, whereas table 2 only has 3. It is possible that this is a sign that "Other" genders are saved in several categories in one table and in less in the other table. When linking this may mean that you have to consider 0 or 9 in table 1 to be a match with 0 in table 2.

        ??? "Blocking Rules Assessment"
            ```py exec="on" result="console" session="blocking_rules"
            import pandas as pd

            address_schema = ['column', 'Null percentage']
            data_table1 = [['given_name', '10%'],['gender', '1%'],['postcode', '30%']]
            address = pd.DataFrame(data_table1, columns = address_schema)
            print(address)
            ```
            In this case, using postcode as a blocking rule may not be appropriate, as due to such low data completeness in the column you might be blocking out records that are the correct match. Given name or gender may be more appropriate, though consideration of the low uniqueness of gender may make it less appropriate.

        ??? "Correlated Values Assessment"
            ```py exec="on" result="console" session="correlation"
            import pandas as pd

            address_schema = ['Unique_ID', 'street', 'postcode', 'outcode', 'city']
            data_table1 = [[1, 'Portland Street', 'LS31BL', 'LS3', 'Leeds'],[2, 'Wellington Place','LS14AP','LS1','Leeds'],]
            address = pd.DataFrame(data_table1, columns = address_schema)
            print(address)
            ```
            In this case, the different address columns are correlated, as they should all work together to get a consistent address. However, for the person with Unique_ID equal to 1, their street name does not align with their postcode, so one of them would be wrong. You need to consider whether you would use just one column for linking on address (e.g. just the postcode) or a hierarchy of the different columns, for example, if postcode does not match, but outcode and street do, how would you consider this?

## Enrichment

Data enrichment is the process of enhancing the quality and usefulness of data for data linkage. It involves transforming, standardising, filtering, and cleaning the data to optimise its value.

!!! info "Data enrichment"

    === "Recommendations"

        - Transform: Create derived variables, recode categories, adjust formats, reshape data structures to ensure compatibility.
        - Standardise: Convert formats (dates, text case), map variable categories, address recording inconsistencies by applying standardisation techniques.
        - Exclude: Protect privacy and accuracy by removing sensitive data, national data opt-outs, and irrelevant fields.
        - Clean: Identify and correct errors, missing values, inconsistencies, and outliers.

        Document the results of data transformations and standardisation to maintain transparency and reproducibility.

    === "RAG"
        &#128308; **RED:** <br>
        There is no structured approach for data transformation.
        If transformations have been applied, they are scattered in the code, and have not been identified or documented.
        No efforts have been made to identify and exclude some sensitive, irrelevant or incorrect data.

        &#128993; **AMBER:** <br>
        While basic procedures for data transformation are in place, they aren't comprehensive.
        Some standardised practices can be observed, but partially documented.
        Efforts have been made to identify and exclude some sensitive, irrelevant or incorrect data, but the approach lacks comprehensiveness.


        &#128994; **GREEN:** <br>
        Data is systematically reviewed for the need of being transformed, standardised, filtered and cleansed.
        The processes are documented and identified in the code.


    === "Worked examples"

        ??? "Transform gender values"
            ```py exec="on" source="above" result="console" session="data_profiling"

            import pandas as pd

            gender_untransformed_schema = ['patient_id', 'gender']

            untransformed_gender_data = [[1001, 1],[1002, 0],[1003, 2],[1004,1],[1005, 1],[1006, 9],[1007, 2],[1008,9]]
            untransformed_gender_df = pd.DataFrame(untransformed_gender_data, columns = gender_untransformed_schema)

            def transform_gender_formatting(df, column_to_standardise):
                '''
                Converts encodings of 9 as 'unknown' for gender to 0
                '''
                df['transformed_gender'] = df[column_to_standardise].replace(9, 0)

                return df

            transformed_df = transform_gender_formatting(untransformed_gender_df, 'gender')

            print("Untransformed gender")
            print(untransformed_gender_df)
            print('\n')

            print(transformed_df)

            ```

            In this example, a decision was made to standardise the gender encodings of '9' of unknown to '0' which codes to unspecified, of which there were some pre-existing values in the table. This standardisation could happen if there are multiple encodings for 'other' in one table, but only one mapping of 'other' in another.

        ??? "Standardise text case"
            ```py exec="on" source="above" result="console" session="data_profiling"

            import pandas as pd

            names_unstandardised = ['patient_id', 'name']

            unstandardised_names_data = [[1001, 'alan'],[1002, 'BOB'],[1003, 'carla'],[1004,'David'],[1005, 'ERIC'],[1006, 'frances'],[1007, 'gReg'],[1008,'Hannah']]
            unstandardised_names_df = pd.DataFrame(unstandardised_names_data, columns = names_unstandardised)

            def standardise_name_formatting(df, column_to_standardise):
                '''
                Converts all text cases to upper case for names
                '''
                df['standardised_name'] = df[column_to_standardise].str.upper()

                return df

            standardised_df = standardise_name_formatting(unstandardised_names_df, 'name')

            print("Unstandardised gender")

            print(unstandardised_names_df)
            print('\n')

            print(standardised_df)

            ```
            In this example, standardising the text case makes linkage easier as variations in capitalisations are removed so 'ALAN', 'alan' and 'Alan' would correctly be treated as the same name.



        ??? "Exclude records for linkage by patient consent"
            ```py exec="on" source="above" result="console" session="data_profiling"

            import pandas as pd

            patient_consent = ['patient_id', 'consent']

            unfiltered_patient_data = [[1001, True],[1002, True],[1003, True],[1004,True],[1005, False],[1006, True],[1007, True],[1008,True]]
            unfiltered_consent_df = pd.DataFrame(unfiltered_patient_data, columns = patient_consent)


            def filter_to_consenting_patients(df, patient_consent_column):
                '''
                Removes any patients who have not consented to be contacted from the linkage
                '''
                return df[df[patient_consent_column]]

            consenting_patients_df = filter_to_consenting_patients(unfiltered_consent_df, 'consent')

            print("Unfiltered patient consent table")

            print(unfiltered_consent_df)
            print('\n')

            print("Table of patients filtered to those who consent to their data being analysed")
            print(consenting_patients_df)

            ```
            In this example, the data is filtered so any patients who do not consent for their data to be used are removed from the cohort to be linked.

        ??? "Clean null name values"
            ```py exec="on" source="above" result="console" session="data_profiling"

            import pandas as pd

            name_uncleaned_schema = ['patient_id', 'name']

            uncleaned_name_data = [[1001, 'alan'],[1002, 'BOB'],[1003, 'carla'],[1004,'David'],[1005, None],[1006, 'frances'],[1007, 'gReg'],[1008,None]]
            uncleaned_name_df = pd.DataFrame(uncleaned_name_data, columns = name_uncleaned_schema)

            def clean_null_name_values(df, column_to_standardise):
                '''
                Converts encodings of null to 'unspecified'
                '''
                df['cleaned_name'] = df[column_to_standardise].fillna('Unspecified')

                return df

            cleaned_df = clean_null_name_values(uncleaned_name_df, 'name')

            print("Uncleaned name table")
            print(uncleaned_name_df)
            print('\n')

            print("Cleaned name table")
            print(cleaned_df)

            ```

            In this example, any null gender values are recoded to 'Unspecified'.


If you have any ideas or feedback you'd like to give the team, feel free to [contact us](<https://github.com/nhsengland/quality-assurance-framework-for-data-linkage/issues/new?assignees=&labels=&projects=&template=send-feedback-on-the-quality-assurance-framework-for-data-linkage.md&title=>)