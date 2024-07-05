---
hide:
  - navigation
---

# Evaluation

## Verification and Validity

Verification ensures that the project is built correctly according to specifications, validation ensures that the project addresses the right problem and delivers the expected results.

!!! info "Verification and Validity"

    === "Recommendations"

        Verification in a data linkage project involves:

        - Ensuring alignment of methods and processes with project specifications

        - Conducting code reviews and unit testing

        - Confirming the robustness of the chosen methodology through expert review

        - Clearly documenting any deviations from requirements

        Validation in a data linkage project entails:

        - Sense checking, comparing results against established truths or manual inspections to verify plausibility with users and data linkage experts.


    === "RAG"
    
        &#128308; **RED:** <br>
        Insufficient practices in verification, validity checks. No established routine for sense checking or peer reviews in data linkage projects.

        &#128993; **AMBER:** <br>
        Intermittent verification and validity checks with some inconsistencies, along with occasional sense checking and peer reviews that may lack consistency.

        &#128994; **GREEN:** <br>
        Verification and validity checks performed. Clear practices and established routines for sense checking and thorough peer reviews.

## Quality of data linkage

Effective evaluation of data linkage quality builds trust in the results and provides a quantitative assessment of the linkage process's impact on subsequent procedures, such as statistics reliant on the linked data.

!!! info "Quality of data linkage"

    === "Recommendations"

        Record-level checks

        - Identifying errors in specific records

        - Analysing metadata like matching steps and confidence scores

        Aggregate-level checks

        - Identifying agreement patterns in linking variables

        - Identifying biases

        - Assessing analytical outcomes' sensitivity to parameter adjustments (if data permits)

        - Cross-referencing outcomes with alternative sources or linkage methods

        Other checks

        - Utilising clerical resources (if available) for structured reviews to establish a ground truth

        - Computing precision, recall, and F1-score (if a ground truth is established)



    === "RAG"
    
        &#128308; **RED:** <br>
        The results of the Data Linkage process have not been evaluated. The impact of the linked data quality is unknown on subsequent procedures.

        &#128993; **AMBER:** <br>
        Partial evaluation of the linked data is available but it inconsistent.

        &#128994; **GREEN:** <br>
        A process to evaluate the data linkage quality is in place and is comprehensive. Users of linked data are aware of the outcomes of this evaluation.

## Speed

Efficient data linkage balances timeliness with accurate results.

!!! info "Speed"

    === "Recommendations"

        - Track processing speed and identify bottlenecks for improvement

        - Tackle factors like dataset size, hardware limitations, and inefficient algorithms

        - Ensure your process can handle larger datasets and increased frequency without sacrificing quality



    === "RAG"

        &#128308; **RED:** <br>
        The linkage process speed has not been assessed. No attempts to improve speed have been made.

        &#128993; **AMBER:** <br>
        Some efforts are made to improve the efficiency of the linkage but partially or not implemented.

        &#128994; **GREEN:** <br>
        Efficient data linkage processes have been achieved through proactive reviews and enhancements.

## Computational Resources Used

Computational resources used refers to the computing infrastructure required to support the Data Linkage process.

!!! info "Computational resources used"

    === "Recommendations"

        - The size of the datasets being linked influences the computational resources - as larger data sets require more processing power and time, memory, and storage.

        - Allocate sufficient computational resources for diverse types of DL projects and optimise processing times to ensure efficient data linkage.

    === "RAG"


        &#128308; **RED:** <br>
        Insufficient computational resources which forces the use of suboptimal linkage methods.

        &#128993; **AMBER:** <br>
        There is allocation of resources, but it is not ideal for complex data linkage projects.


        &#128994; **GREEN:** <br>
        Adequate allocation of computational resources for different types of DL projects to minimise the linkage error.

    === "Worked examples"

        ??? "Function to measure the run time of a function"
            ```py exec="on" source="above" result="console" session="data_profiling"

            import timeit
            import time

            def measure_function_time(f):
                '''
                Times how long a function takes to run in seconds
                '''

                start_time = timeit.default_timer()
                f()
                end_time = timeit.default_timer()
                print(f"It took {end_time-start_time}s to call the function")


            def wait_15_seconds():
                '''
                Function called to wait 15 seconds before executing print statement
                '''
                time.sleep(15)
                print('Waited 15 seconds!')

            measure_function_time(wait_15_seconds)

            ```

            Understanding how long a function takes to run can be used to understand resource allocation in your machine, and can be used as a proxy to understand the load in different parts of the data linkage process.

        ??? "Function to measure CPU usage"
            ```py exec="on" source="above" result="console" session="data_profiling"

            import psutil

            def get_cpu_usage(time_period):
                '''
                Prints the CPU usage over a time period
                '''

                cpu_usage = psutil.cpu_percent(time_period)
                return cpu_usage

            time_period = 10

            print('The CPU usage for the last',time_period,'seconds is : ',get_cpu_usage(time_period))

            ```
            Understanding how CPU is being used helps understand resource allocation in your machine, and can be used as a proxy to understand the load of different data linkage models

        ??? "Function to measure the ram memory being used"
            ```py exec="on" source="above" result="console" session="data_profiling"

            import psutil

            def get_ram_memory():
                '''
                Returns the % of RAM being used, and number of GB being used by RAM at a moment in time
                '''

                ram_percentage_used = psutil.virtual_memory()[2]
                ram_gb_used = psutil.virtual_memory()[3]/1000000000
                return ram_percentage_used, ram_gb_used


            print(get_ram_memory())
            ```
            Understanding how RAM is being used helps understand resource allocation in your machine, and can be used as a proxy to understand the load of different data linkage models
