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
2. VAF analysis
   * Dynamics of mutation frequencies
   * VAF groups analysis in different cell lines
3. Allele-specific mutations analysis

## Results
### Part 1
1. WES file is more like a reference data, RNA seq is more like expression.
2. The task of determining which WES file which RNA was reduced to the task of binary classification: reference or not. For additional quality control, an additional classification was carried out: expression data or not. 
3. To assess the quality, $F_{\beta}$ score was used, with the $\beta$ parameter equal to 1.4, since the specificity of the methods is important in this task
4. Thus it turned out to determine the type of files
![image](https://user-images.githubusercontent.com/98456969/230784789-d890af7e-9619-4bed-ac2f-e780f525e5c3.png)


### Part 2
1. Consideration of polymorphism of ordinary cells. Joined WES and RNA data for each purity for both cell lines.
2. Identification of the type of VAF mutations via purity dependence. VAF plots with colour annotation. <br>
No correlation from purity - "Stable", the presence of VAF correlation from purity - "Decreasing" label. <br>
FDR control (B-Y), $\alpha = 0.1$
![image](https://user-images.githubusercontent.com/98456969/230784723-b929313d-7c6b-4101-91f9-ea4b190e8770.png)

3. Group selection <br>
Hypothesis: mutations stable from dilution are a characteristic of tumor tissue. <br>
Check: 
    * The intersection of stable mutations and the corresponding genes of the COLA and NCC lines was empty
    * Literature data on stable mutations confirmed the connection with a characteristic tumor: COLO - melanoma, HCC - sarcoma
4. COLO's GO correlates with membrane, Golgi functions.
5. HCC's GO correlates with cytoplasm cell projection, signal transduction, synapse, nucleus.

### Part 3
1. VAF DNA is an indicator of zygosity and heterogeneity in somatic mutations, which we are studying
2. Using VAF DNA, we determine the baseline for the heterozygote. Then we look at the VAF RNA to see how much the expression of this gene changes.
3. VAF RNA is not really an indicator of expression, it is also an indicator of zygosity and heterogeneity, but it depends on expression. Because expressions can go unevenly from two alleles.
4. We start with a simple assumption that 50% of mutations in 100% breeding are heterozygotes.
![image](https://user-images.githubusercontent.com/98456969/230784748-561774f0-225a-4a39-a48d-2e9f6c9bcf0c.png)

6. Using VAF DNA, we determine the baseline for the heterozygote. Then we look at the VAF RNA to see how much the expression of this gene changes.
7. We consider suspicious those mutations in which the absolute difference between DNA and RNA VAF is more than 0.15
9. In the HCC data, a subclone is distinguished: on the data on 100% dilution, it is clear that the median is in the region of 0.2 VAF DNA
![image](https://user-images.githubusercontent.com/98456969/230784871-41f0e701-1907-4554-b21a-e4ddcab3d85d.png)
![image](https://user-images.githubusercontent.com/98456969/230784889-17dbfad1-32a2-4fca-b736-06e234761fb9.png)


## Conclusions
* At a qualitative level, it turned out to distinguish
between RNA and WES files
* The dynamics of mutation frequencies depending on the
breeding of cell lines has been studied
* Allele-specific mutations have been identified
  * Stable COLO: ALS2, ABCB5, PLD3, CECR2
  * Stable HCC: NET1, OPHN1
* There was no literature evidence of the characteristic allele-specificity of these mutations in specific tumors



## In repo
MAF files that are sources for analysis cannot be shared, only a notebook with a specific data analysis is in the repository, write to the [Marfa](mailto:marfuta.zak@gmail.com) for all questions and remarks
