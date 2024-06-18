# PredictiveTox
A series of tools for the predective toxicity of chemical compounds: I considered a solvent interacting with molecules containing phosphoric acid groups, fr_phos, (or easter groups). This could be become relevant for reactions involving phosphorus containing compounds. I also considered that it may be relevant to include aromatic compounds, aromatic_carbocycles, to their unique properties of solvating power and low reactivity. Effectively, knowing the number of aromatic carbocycles in a solvent molecule could provide insights into its solvation behaviour and compatibility with aromatic solutes. I also considered the LogP value, MolLogP, which can provide information about its hydrophobicity or lipophilicity, which can influence its solubility behaviour and interactions with solutes (solvents with higher LogP values tend to dissolve nonpolar compounds more readily). In addition I considered the partial charges on atoms in a solvent molecule, PEOE_VSA1, as solvents with different charge distributions may interact differently with solutes, affecting solubility, dissolution rates, and other solvent-solute interactions. Lastly different molecular fingerprints are used to compare solvents based on their structural features and identify similarities or differences that may impact their suitability for specific applications.

I used the rdkit package in Python, and added the following features for each molecule that could help in toxicity prediction.
##	fr_phos 
(Number of phosphoric acid groups + phosphoric ester groups in the molecule) This is basically (Fragments.fr_phos_acid(mol) + Fragments.fr_phos_ester(mol) ) where ‘mol’ is an rdkit molecule object and ‘Fragments’ is a rdkit module under ‘Chem’ package.
##	aromatic_carbocycles (Number of aromatic carbocycles in the molecule) 
Computed using Lipinski.NumAromaticCarbocycles(mol) where ‘mol’ is an rdkit molecule object and ‘Lipinski’ is a rdkit module under ‘Chem’ package.
##	MolLogP 
This refers to the Wildman-Crippen LogP value of a molecule. Computed using Crippen.MolLogP(mol) where ‘mol’ is an rdkit molecule object and ‘Crippen’ is a rdkit module under ‘Chem’ package.
## PEOE_VSA1 
is another descriptor value of a molecule computed using the ‘MolSurf’ module under rdkit ‘Chem’ package.
##	Molecule Fingerprint 
a way of encoding the structure of a molecule. It is a series of binary digits (bits) that represent the presence or absence of particular substructures in the molecule. Each fingerprint bit corresponds to a fragment of the molecule. The presence of some specific types of substructures in a molecule could determine the toxicity of a molecule. Hence, the fingerprint does that job of encoding the graph structure of a molecule as a vector of bits where each bit could be individually passed as a feature to our classifier. 

I considered four classification methods, logistic regression, random forest, gradient boosting and a forward pass neural network.
## Logistic Regression:  
I assumed a linear relationship between the features and the log-odds of the target variable (including independence of observations). I used a regularization parameter (C) which controls the strength of regularization, influencing the trade-off between fitting the training data and preventing overfitting.
## Random Forest: 
an  ensemble method based on decision trees, making fewer assumptions about the data distribution. Key parameter considered is max depth (maximum depth of each tree), which influenced the model's complexity and ability to capture patterns in the data. 
## XGBoost: 
used as an ensemble method based on decision trees, thus making fewer assumptions about the underlying data distribution compared to linear models. The key parameters included learning rate (controls the step size during training) and max depth (maximum depth of each tree), which influenced the model's complexity and ability to capture patterns in the data. Its implementation can be seen in figure 7.
## Neural Network: 
key parameters considered included the learning rate (controls the size of the step taken during optimization) and the number of epochs (number of times the entire dataset is passed forward and backward through the network during training).
