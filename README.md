# Mutations analysis in transcription data. Allele specific expression
## Authors:
* Marfa Zakirova
* Anastasiya Yudina
## Introduction 
A number of single nucleotide substitutions (SNPs) and short deletions or insertions (indels) may be present in tumor cells. We can identify these mutations from the NGS data. It is important to be able to determine not only the physical presence of alterations in the genome, but also its expression, which primarily determines the effect on the cell.

## Aim
There is targeted therapy for some point mutations, i.e. the decision on further treatment of the patient will largely depend on whether we have found certain mutations in the NGS data of the clinical sample. It is important to take into account the expression of the variant, since the absence of expression of the variant can lead to a lack of effect from therapy. Thus, the task of setting up mutation search pipelines, integrating DNA and RNA sequencing data, filtering possible artifacts and evaluating quality metrics is one of the important stages of bioinformatic analysis of NGS data.

## Workflow
1. Detection of transcription data
   * Сlassification problem
