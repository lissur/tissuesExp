# tissuesExp

## Description

The objective of the tissuesExp pipeline is to create the tissuesExp database. This database was designed to provide support to answer the question "In whose tissues does a given gene have a distinct expression?" based on RNA-Seq experiments.

The pipeline was built as an RMarkdown document constituted by 32 chunks. The Rmd file (RMarkdown) is an R notebook that allows the execution of blocks of code (chunks) in a particular order. To run a specific chunk, click on the "Run Current Chunk" button in the upper right corner of the desired chunk.

The pipeline inputs are a tsv file containing the data and a tsv file containing the metadata for the RNA-Seq experiment. The data must be in the format genes in the rows and tissues in the columns with the gene expression given in TPM. It is not necessary to download the input files, you just need to provide the [ArrayExpress](https://www.ebi.ac.uk/arrayexpress/) code ([ATHAR et al., 2019][ATHAR et al., 2019]) for the RNA-Seq experiment as described in step 4 of the topic "Usage".

The pipeline performs all the analyzes and generates all the tables of the database.

## Example

The provided Rmd file was formatted to generate the database for the RNA-Seq experiment ["Variation in RNA expression in a panel of 30 breast cancer cell lines"](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-4801/Results) ([JASTRZEBSKI et al., 2018][JASTRZEBSKI et al., 2018]) serving as an example.

## Usage

1. Create the directory structure with a folder for the Rmd file and a folder for the tsv files.

2. Save the Rmd file in the folder for it.

3. Open the Rmd file in RStudio.

4. Set the pipeline variables in the chunk "3. Pipeline variables".

    rnaseqExpName: name of the RNA-Seq experiment, which will be used as a prefix for the names of the tables in the database  
    rnaseqExpCode: [ArrayExpress](https://www.ebi.ac.uk/arrayexpress/) code ([ATHAR et al., 2019][ATHAR et al., 2019]) for the RNA-Seq experiment  
    database: name of the database to be created  
    pipelineDir: directory containing the Rmd file, as defined in step 1 above  
    rnaseqExpDir: directory containing the tsv files, as defined in step 1 above  

5. Run the pipeline. You must run specific blocks of code (chunks) in a specific order three times as detailed below. In each run, you should set the chunks variables in the chunk "4. Chunks variables" before running the chunks. The chunks to be executed can be recognized by their numbers or by their identifiers and they can be executed by clicking on the "Run Current Chunk" button in their upper right corner.

	First run
  
		Chunks variables: consideringOutliers = "yes", fence = "inner"
    
		Chunks numbers: 1-10, 15-18, 23-24, 27, 29
    
		Chunks identifiers: setup, libraries, pipeline_variables, chunks_variables, download_data, download_metadata, create_database, tpm, tpm_max, metadata, avg_std, normality_test, uniformity_test, zeros_counting, tsScore, tge, kurtosis_skewness, gte50
    

	Second run
  
		Chunks variables: consideringOutliers = "no", fence = "inner"
    
		Chunks numbers: 4, 11, 15-17, 19-22, 27
    
		Chunks identifiers: chunks_variables, boxplot, avg_std, normality_test, uniformity_test, tests_summary, oScore, oScore_max, fences, kurtosis_skewness
    

	Third run
  
		Chunks variables: consideringOutliers = "no", fence = "outer"
    
		Chunks numbers: 4, 11-12, 14-17, 25-28
    
		Chunks identifiers: chunks_variables, boxplot, outliers_summary, outliers_count, avg_std, normality_test, uniformity_test, tpm_oScore_tsScore_outliers, herd, kurtosis_skewness, kurtosis_skewness_summary
    

6. (Optional) Run the chunk "31. Session information" to get the R session information.

7. Run the chunk "32. Remove pipeline variables" to remove the pipeline variables.

[ATHAR et al., 2019]:https://pubmed.ncbi.nlm.nih.gov/30357387/
[JASTRZEBSKI et al., 2018]:https://pubmed.ncbi.nlm.nih.gov/29844118/
