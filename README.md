# ARDS YOUNG 

This repository performs ards young analysis on data at different sites and reports the results in the [`results/`](results/) folder.

## Preliminary

### Procedure: 

-1- List the procedure used for the severe definition  in the following file 
   https://docs.google.com/spreadsheets/d/1MSp2_h2f9F3wMc6iLg85nZwhkCHGiMrV8gM8s7rSaP4/edit#gid=0

-2- 
   Option 1 : Your institution use the ICD-10-PCS Procedure classification for the procedure 
              Make sure that procedure code are included in your LocalPatientObservations.csv file((Phase 2.1))
    => Go to the next section 

    Option 2 : Your institution is using a different procedure classification 
               Map the local procedure code to the PROC-ICD10 in the google sheet 
               https://docs.google.com/spreadsheets/d/1MSp2_h2f9F3wMc6iLg85nZwhkCHGiMrV8gM8s7rSaP4/edit#gid=0
               In your LocalPatientObservations.csv replace your local code by the one from the ICD-10-PCS Procedure classification
               Do not forget to add the concept_type ="PROC-ICD10"

=> Go to the next section 


### Blood gas 
Make sur that the Pa02(loinc 2703-7) and PaC02 (loinc 2703-7) are included in your LocalPatientObservations.csv file

### QC analysis: 
Validate  the QC analysis for the your phase 2 and 1 files
https://github.com/covidclinical/Phase2.1DataRPackage


## Which script should I run?

The best way to run this analysis is to clone this repository on your local machine
(please ensure you're in a directory where you want the repository to be downloaded):

```git clone https://github.com/bertrandmoal/ards_young.git```

Then, go inside the repository:

```cd ards_young```

and make a copy of `ards_young_analysis.Rmd`, name it with your site name, for example:

```cp qards_young_analysis.Rmd ards_young_analysis-frbdx.Rmd```

and open the R project

```open ards_young.Rproj```

and navigate to the newly created file (e.g. `ards_young_analysis-frbdx.Rmd`) to modify the code to run on the data at your specific site.

line 1 - change the site name in the title
line 13 -  output_file="ards_young-frbdx.html" => change with your site name
line 52-53-54 -  change the path to load the phase 2 files 
line 59 - indicate if there is an obfuscation required ( TRUE or FALSE)
line 62 - if YES what is the level of obfuscation ( number) 

Once everything runs, please hit the "Knit" button on top of the `.Rmd` file to create an `.html` file that will automatically be put into [`htmls/`](htmls/).

## What are the results?

There will be 5 outputs 
ards_young-{sitei}.html 
ards_young_day_{sitei}.csv
ards_young_gen_{sitei}.csv
ards_young_lab_{sitei}.csv
ards_young_proc_diag_med{sitei}.csv

for the analysis, 6 groups were considered 
- ARDS_18_49 : patients with ICD10/9 code for ARDS between 18 and 49 years old 
- ARDS_sup_49 : patients with ICD10/9 code for ARDS older than 49 
- NO_ARDS_18_49 : patients without ICD10/9 code for ARDS,  without severe procedure, without severe medication, between 18 and 49 years old .
- NO_ARDS_sup_49 : patients without ICD10/9 code for ARDS,  without severe procedure, without severe medication, older than 49 .
- OTHERS_18_49 : patients without ICD10/9 code for ARDS,  with severe procedure or with severe medication, between 18 and 49 years old  .
- OTHERS_49 : patients without ICD10/9 code for ARDS,  with severe procedure or with severe medication, older than 49 .

In addition distinction between patients included between Januray and July vs August and December was done 

ards_young_day_{sitei}.csv : number of patient by day and by groups 

ards_young_gen_{sitei}.csv by groups
- number of patient, in total, by age groups and by sex 
- mean and std of number of ICD10/9, Medication, Procedure and Loinc code
- mean and std length of stay 
- number of severe patient 
- number of patient with a previous hospitalization 
- number of patient with a rehospitalization 
- number of dead, dead in less than 28 and 90 days, out the hopistal in less than 28 and 90 days

ards_young_lab_{sitei}.csv : number, mean, and std lab by day and by groups 

ards_young_proc_diag_med{sitei}.csv
number of patients with ICD10/9, medication, procedure by groups 

Finally, please upload your results (in [`results/`](results/) and [`htmls/`](htmls/)) via a [pull request] or request @bertrandmoal to add you as a contributor.

If you run into any problem adapting this code to your data, let us (@bertrandmoal) know via Slack
