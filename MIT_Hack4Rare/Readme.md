#In-Silico Repositioning of Drugs for Neurofibromatosis 2 Vestibular Schwannoma using Machine Learning 
## Team   - **MedBot**
---
## Team members
1. Kshitij Mohan - Undergrad Student, IIIT Delhi
2. Pranav Goyal - Undergrad Student, IIIT Delhi
3. Parikshit Sen - Undergrad student, Maulana Azad Medical College
4. Aiman - Undergrad student, Maulana Azad Medical College
5. Dr. Amritpal  - Junior resident Maulana Azad Medical College
6. Dr. Manu K Shetty - Associate Professor (Pharmacology), Maulana Azad Medical College
---
Neurofibromatosis type 2 is an autosomal-dominant multiple neoplasia syndrome. It is highly debilitating with the frequency of one in 25,000 live births and nearly 100% penetrance by 60 years of age (1). NF2 represents a difficult management problem with most patients facing substantial morbidity and reduced life expectancy. The hallmark of NF2 is the appearance of bilateral vestibular schwannomas, benign tumors on both sides of the vestibular nerve. People with NF2 may also develop schwannomas in other parts of the body, or may develop other types of benign brain or spinal tumors (2) .At this time, possible treatments available for Neurofibromatosis 2-associated tumors include surgery, chemotherapy, and radiation therapy (3).  Presently available off-label drugs are not fully effective. It has also been observed that monotherapy is not effective with lesser efficacy, higher resistance and toxicity. The complex interlinked pathways in the pathogenesis NF2 suggest multi-drug therapy may provide an ideal therapeutic effect (4).  We therefore would like to work on developing a Machine Learning model  to identify suitable drug combination that could lead to better efficacy and lesser chance of resistance. 

At Present huge dataset is available to the scientific community. These datasets focused on many aspects of drug discovery and development, ranging from chemical representational of the drug to parallel biochemical assays results. The 3D structure of the protein and binding sites information is available, this data used to understand the drug specificity.  Development of high-throughput screening of target on large list of molecules progress in assay miniaturization.  In the database like ChEMBL or PubChem millions of experimental data on drug–target interactions are available in and that can be used for in-silico drug–target profiling. With current advance in machine learning, many studies are undertaking in selecting lead molecule from large datasets of chemical entities by in-silico screening. Future drug development in-silico screening can be streamlined for hit identification and lead development (5).

---
## Methods
Steps 
1. Create a dataset that can be used to assign a score to the interaction of drugs and targets.
2. Design an encoding method to encode the data that preserves the sequential features of the target.
3. Gather physical and chemical features of the of drugs.
4. Create a Neural Network that is able to learn the features and predict the affinity accurately.

We have solved the Drug-Target Interaction problem as a regression task. To handle the data distribution shifts well, we needed to build a model that is neither too complex (high accuracy, low robustness) nor too simple (low accuracy, low robustness). Thus, we used a multi-head CNN with attention layers, which proved to be ideal. In contrast to the recent more advanced architectures like Graph Neural Networks, Transformers, etc. CNN had the best validation measures for the data and features we had.

Our Dataset is based on 2 datasets that are kiba dataset and davis dataset respectively. These datasets contained the molecular formula of the drug, the protein sequence of the target, and corresponding affinity scores. We first used the PubChemPy library to extract some of the drug's important physical and chemical features using their molecular formula and added them to the dataset. Then we also label encoded the protein sequence and molecular formula for easier use. First, we had performed a 85-15 train-validation split on our dataset while ensuring the sets of proteins to be disjoint in train and validation sets.  Trained model tested on validation dataset. 
The affinity score ranges from 0-17.2 where higher score denotes higher interaction. Around 50% of affinity scores are near 12 whereas 95% of the affinity scores are between 10-13.



#### Target selection for testing: 
All NF2 pathways and targets are listed. A further target is shortlisted by considering the following features 
         a.	Distribution of target in the body
         b.	Location of the targets (intracellular or extracellular) 
         c.	Over-expression or under-expression 
         d.	Proven evidence of target involved in diseases 
Using our ML model selected targets are screened in the drug list

#### Model architecture
We built a multi-head CNN with 4 heads corresponding to drug properties, drug label encodings, protein ngrams, and protein label encodings. First we encoded each of these features into low dimensional feature maps. By doing so, we ensured that: 1) The important features are retained before final few layers of feature interactions. 2) Curse of dimensionality is avoided altogether and the model doesn't overfit. For obtaining these encodings, convolution, attention and batchnorm layers were used along with dropout. Next we concatenated the encoded feature maps and performed feature interaction with the help of few linear layers.


---
## Results
We divided the whole data into train (85%) and validation (15%) datasets. Data was used to train the neural network. 
Our model achieved  
* Mean square error:  0.761   
* R_Square Score:  0.206

---

---

## Silent features of our model 
* Model can be used for in-silico screening for any target. And drug lists can be selected based on our requirements. 
    * 	Only FDA-approved drugs
    * 	FDA approved drugs  and drugs under clinical trails 
    * 	All drugs present in the database PubChem. 
* 	Model helps in finding the docking or binding affinity of the drug to the target 
* 	Model  also indirectly helps in predicting the safety of the drug (by predicting the drug binding affinity with all protein-target families )

---
## Future directions
Currently, we are able to extract limited features from the amino acid (protein) sequence. 3D protein structures are known to provide rich and extra information about proteins. Alphafold is a recent breakthrough that has been able to achieve protein folding highly accurately. By using the 3D structures from the Alphafold database, we will be equipped with much more information than we currently have. There will also be an increase in the resembling structures shared by known and unknown proteins. Thus we will have richer data that better resembles the unknown target data. With the availability of better data, we plan to move on to use advanced neural networks such as Graph neural networks, Transformers, etc. Overall, we would see significant improvement in our models performance.

Our model used to identify potentially active molecules for the selected NF2 target. Further target-drug pair prioritisation is done considering the target and drug features. Drugs parameter includes; drug approval status, safety, lipid solubility, evidence in literature and Drug interaction.  From the shortlisted drug-target pain  for each target different drug combination would be tested for in-vitro efficacy studies. 
One advantages of the model is that, our model able to predict the affinity of  selected drug with all protein-target families, critical for predicting the drug safety analysis.


---
## References
1.	Asthagiri AR, Parry DM, Butman JA, et al. Neurofibromatosis type 2. Lancet. 2009;373(9679):1974-1986. doi:10.1016/S0140-6736(09)60259-2 
2.	Tiwari R, Singh AK. Neurofibromatosis Type 2. [Updated 2020 Aug 10]. In: StatPearls [Internet]. Treasure Island (FL): StatPearls Publishing; 2021 Jan-. Available from: https://www.ncbi.nlm.nih.gov/books/NBK470350/
3.	Dirks MS, Butman JA, Kim HJ, et al. Long-term natural history of neurofibromatosis Type 2-associated intracranial tumors. J Neurosurg. 2012;117(1):109-117. doi:10.3171/2012.3.JNS111649
4.	Fuse MA, Plati SK, Burns SS, et al. Combination Therapy with c-Met and Src Inhibitors Induces Caspase-Dependent Apoptosis of Merlin-Deficient Schwann Cells and Suppresses Growth of Schwannoma Cells. Mol Cancer Ther. 2017;16(11):2387-2398. doi:10.1158/1535-7163.MCT-17-0417
5.  Brogi S, Ramalho TC, Kuca K, Medina-Franco JL, Valko M. Editorial: In silico Methods for Drug Design and Discovery. Front Chem. 2020 Aug 7;8:612. doi: 10.3389/fchem.2020.00612.

---
## Project Pitch
[Presentation slides](https://www%2Ecanva%2Ecom/design/DAElkwoJipM/vn5SrsbTh0tqAm8g0YryXw/view%3Futm%5Fcontent%3DDAElkwoJipM%26utm%5Fcampaign%3Ddesignshare%26utm%5Fmedium%3Dlink%26utm%5Fsource%3Dsharebutton)
[Presentation video](https://drive%2Egoogle%2Ecom/file/d/1ffCcEu1wn4cXMN7kgJoTvmpXjd%2DsEx5L/view)
---
## Team
