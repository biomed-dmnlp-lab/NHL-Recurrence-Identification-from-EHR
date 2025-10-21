<h1>Guide to understanding code in the project</h1>

<h2> Table of Contents </h2>

- [**Note**](#note)
- [**EDA and Data Processing Notebooks**](#eda-and-data-processing-notebooks)
  - [EDA.ipynb](#edaipynb)
  - [ClinicalNotesSentenceSplitter.ipynb](#clinicalnotessentencesplitteripynb)
- [**ML and LLM Pipleine(s) Code**](#ml-and-llm-pipleines-code)
- [**Final Pipeline**](#final-pipeline)




## 🔴<code style="color : red">**Note**</code>
1. All the "requirements.txt"(python environment required to run code) to the notebooks or .py file are found in their respective folders.
2. Because of the sensitive nature of the datasets involved datasources are not included in the repo.

## <code style="color : Orange">**EDA and Data Processing Notebooks**</code> 

### <code style="color : Yellow">EDA.ipynb</code>

**This notebook is initial step to running the project.**

This notebook contains exploratory data anlysis, pre-processing, cleaning and intial datasets creation for machine learning(tabular) and llm (clinical) used in ML and LLM Pipline(s) code.


 

**Input files required**:
Intially the project uses data from vdw which is converted to csv files. Below, u can find the file names and column names.



**Output files**:
1. <code style="color : Green">NHL_modeling_dataset_only_tabular_WITH_CPT_v2_with_flt_date_meds_ATC.parquet</code>(Tabular machine Learning)
2. <code style="color : Green">NHL_modeling_dataset_only_tabular_WITH_CPT_v2_with_flt_date_meds_ATC.parquet</code>(Tabular machine Learning)
3. <code style="color : Green">nhl_data_clinical_notes_only_all_note_types_with_cli_dates.pkl</code> (Only Clinical notes for LLM RAG appraoch)

**Tabular ML Features**:
1. Medications (Categorical: ATC level or Active Ingrident; One hot encoded)
2. Lab results (Numerical + Categorical)
3. Diagnoses Codes (Categorical: PheWas; One-hot encoded)
4. Procedure Codes (One-hot encoded)

**LLM RAG Dataset**:
1. Clinical Notes


### <code style="color : Yellow">ClinicalNotesSentenceSplitter.ipynb</code>

**This notebook takes output from "EDA.ipynb" as input to create input for "RAG Notebook" in [ML and LLM Pipleine(s) Code](#ml-and-llm-pipleines-code)**

This notebook contains code for converting clinical notes associated with certain data window for a given patient into individual sentences(chunking).

**Model used**: sentence_detector_dl_healthcare (https://nlp.johnsnowlabs.com/2020/09/13/sentence_detector_dl_healthcare_en.html)

**Input files required**:



## <code style="color : Orange">**ML and LLM Pipleine(s) Code**</code>



## <code style="color : Orange">**Final Pipeline**</code>

The .py file contains code for end to end pipeline i.e code to obtain recurrent patient ids along with data window and clinical notes used for making decision using RAG pipeline(the best approach so far).

**Input data requirements**:

**The pipleine has two modes**:
1. "Evaluate" (To evaluate approach by obtaining metrics) 
2. "Deploy" (No metrics calculated)


**Output format**: json format.
```json
{
  "Patient ID": xxx,
  "Model Output": "Yes/No",
  "Clinical Notes used as evidence": list of clinical notes,
  "Ground Truth Recurrence": "Yes/No " #(This is not present in Deploy mode)
}
```


