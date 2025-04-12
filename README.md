# PFF_Progression_Model  
**Mathematical models for PFF Progression**  
  
**_Yuanxi Li, et al., Key Connectomes and Synaptic‐Compartment‐Specific Risk Genes Drive Pathological α‐Synuclein Spreading. Accepted by Advanced Scince, 2025._**  

Matlab was used for modeling and fitting, Python was used for visualizing figures.  
****
**Matlab: R2021b**  
  
**Python: 3.9.11**  
Packages:  
matplotlib - 3.5.1, matplotlib-inline - 0.1.3, matplotlib-venn - 0.11.9  
numpy - 1.22.3, pandas - 1.4.1, seaborn - 0.11.2


## Modeling and fitting
**I. Global spread model (without gene expression effect), Fig. 2**  
We used _Nexis:global_ [1] as the global spread model to investigate the pathological progression including the amplification, clearance, and spreading of pathological α-Syn. To accommodate a continuous measure of net directional preference, the original _Nexis:global_ [1] was augmented by introducing a new parameter, s, to indicate transmission direction.    
**Run in Matlab:** PFF_Global = PFF_GlobalModel;  
  
**Result Description:**   
data - pathology distribution observed in IHC experiments  
time_stamps - MPI information  
predicted - pathology distribution predicted by the model  
param_fit - parameters after fitting: 1, seed scale; 2, amplification/clearance; 3, spreading effect; 4, directionality; 5-7, not fit.  
results - data_means, average of data; Corrs, Pearson's correlation coefficient between predicted and real pathology over each MPIs; Corrs_Mean, average of Corrs; LogCorrs, Pearson's correlation coefficient between log10(predicted) and log10(real pathology) over each MPIs; LogCorrs_Mean, average of LogCorrs; LinR, Lin's concordance correlation coefficients [2] between predicted and real pathology over each MPIs; LinR_Mean, average of LinR; New_R_Log, we defined a new loss function, not using here; LogLinR, Lin's concordance correlation coefficients [2] between log10(predicted) and log10(real pathology) over each MPIs; LogLinR_Mean, average of LogLinR; sse_individual, sum of squared errors measured by predicted and real pathology data over each MPIs; sse_all, average of sse_individual;   
  
To test specific directionality parameters, please modify Line 105-Line 110 in "PFF_GlobalModel.m" file. E.g., to test unbiased retrograde, modify all three values to 0.5 and rerun the model.  
****
**II. Test random connectomes on global spread model, Fig. 3A**  
Test if random artificial connectomes (‘null models’) could predict pathological α-Syn progression on global spread model, repeated 1,000 times.  
**Run in Matlab:** TestRandomConnectome = PFF_TestRandomConnectome;  
****
**III. Test permutated connectomes on global spread model, Fig. 3B**  
Test the case when elements of the whole connectome were randomly permutated. We repeated more than 1,000 times, but we only took the first 1,000 results for analyses, since there were some cases that couldn't be fit.  
**Run in Matlab:** TestPermutatedConnection = PFF_TestPermutatedConnection;  
****
**IV. Test randomly removed different proportions (5%~95%) of the actual connectome, Fig. 3, C-D**  
We randomly removed different proportions (5%~95%) of the actual connectome and evaluated how well the remaining partial connectome can predict pathological α-Syn transmission, repeating each case 1,000 times for robustness. We repeated each more than 1,000 times, but we only took the first 1,000 results for analyses, since there were some cases that couldn't be fit.    
**Run in Matlab:** TestPartialConnectome_RatioFrom5to95 = PFF_TestPartialConnectome_RatioFrom5to95;
****
**V. Test the cases of removing different proportions of the strongest or weakest connections, Fig. 3, E-F**  
We removed different proportions of the strongest or weakest connections from the connectome.  
**Run in Matlab:**  
TestPartialConnectome_RemoveWeakest = PFF_TestPartialConnectome_RemoveWeakest; (Fig. 3E)  
TestPartialConnectome_RemoveStrongest = PFF_TestPartialConnectome_RemoveStrongest; (Fig. 3F)  
****
**VI. Gene models of outgoing, incoming, and combined effects, Fig. 4**  
See **Methods** for details.  
**Run in Matlab:**  
TestGenes_Outgoing = PFF_TestGenes_Outgoing;  
TestGenes_Incoming = PFF_TestGenes_Incoming;  
TestGenes_Combined = PFF_TestGenes_Combined;  
****
**VII. Robustness test for 500th-ranked-gene for outgoing, incoming, and combined effects, Fig. 6A, Fig. S14**  
In order to ensure that these genes all had robust performance in predicting the spread of pathological α-Syn, we conducted bootstrap analyses for each group’s 500th gene (500th-ranked-gene for the outgoing, incoming, and combined effects were _Large_, _Socs6_, and _Tbc1d14_, respectively) by randomly permuting the elements of the gene expression values for 1,000 times.  
**Run in Matlab:**  
TestGenes_Outgoing_BootstrapFor500th = PFF_TestGenes_Outgoing_BootstrapFor500th;  
TestGenes_Incoming_BootstrapFor500th = PFF_TestGenes_Incoming_BootstrapFor500th;  
TestGenes_Combined_BootstrapFor500th = PFF_TestGenes_Combined_BootstrapFor500th;  
****
  
## Visualization
**Run in Jupyter Notebook:**  PFF Data and Results/Figures Python/, *.ipynb files

## Other files
**Comparisons of pathology distribution between 3 and 6 MPI, Fig. S2**  
**Run in Matlab:** GetDifferencePValue.mlx  

## References  
[1] Anand, C., P.D. Maia, J. Torok, C. Mezias, and A. Raj. 2022. The effects of microglia on tauopathy progression can be quantified using Nexopathy in silico (Nex is) models. Scientific Reports 12:21170.  
[2] Lawrence, I., and K. Lin. 1989. A concordance correlation coefficient to evaluate reproducibility. Biometrics 255-268.
