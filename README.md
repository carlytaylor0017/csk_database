# Building a scalable database of chemical names and structures from simplified molecular-input line-entry system (SMILES) strings 
## Carly Wolfbrandt

### Table of Contents
1. [Introduction](#Introduction)
    1. [Skeletal Formulas](#skeletal_formulas) 
    2. [SMILES](#SMILES)
2. [Background](#Background)
3. [Question](#Question)
4. [Data](#Data)
    1. [Cleaning the SMILES Data](#smiles_data)
    2. [Matching SMILES Strings to Skeletal Formulas](#skeletal_images)
    3. [Matching SMILES Strings to IUPAC Names](#iupac_names)
5. [Future Work](#future_work)

## Introduction <a name="Introduction"></a>

### Skeletal Formulas <a name="skeletal_formulas"></a>

The skeletal formula of a chemical species is a type of molecular structural formula that serves as a shorthand representation of a molecule's bonding and contains some information about its molecular geometry. It is represented in two dimensions, and is usually hand-drawn as a shorthand representation for sketching species or reactions. This shorthand representation is particularly useful in that carbons and hydrogens, the two most common atoms in organic chemistry, don't need to be explicitly drawn. These structural formulas contain the same information that the SMILES strings contain, but are depicted in a different way.

**Table 1**: Examples of different chemical species' names, molecular formulas and skeletal formulas

| Common Name      | IUPAC Name |Molecular Formula | Skeletal Formula | 
| :-----------: | :-----------:| :-----------: | :----------:| 
| ethanol      |  ethanol | CH<sub>3</sub>CH<sub>2</sub>OH | ![](images/ethanol.png) |
| acetic acid   | ethanoic acid | CH<sub>3</sub>COOH  |![](images/acetic_acid.png)|
|cyclohexane | cyclohexane | C<sub>6</sub>H<sub>12</sub>| ![](images/cyclohexane.png)  |
| diphenylmethane | 1,1'-methylenedibenzene | (C<sub>6</sub>H<sub>5</sub>)<sub>2</sub>CH<sub>2</sub>|![](images/diphenylmethane.png)|

### Simplified Molecular-Input Line-Entry System (SMILES) <a name="SMILES"></a>

SMILES is a line notation for describing the structure of chemical elements or compounds using short ASCII strings. These strings can be thought of as a language, where atoms and bond symbols make up the vocabulary. 

SMILES strings use atoms and bond symbols to describe physical properties of chemical species in the same way that a drawing of the structure conveys information about elements and bonding orientation. This means that the SMILES string for each molecule is synonymous with its structure and since the strings are unique, the name is universal. These strings can be imported by most molecule editors for conversion into other chemical representations, including structural drawings and spectral predictions. 


**Table 2**: SMILES strings contrasted with skeletal formulas

| Common Name      | IUPAC Name |Molecular Formula | Skeletal Formula |  SMILES String |
| :-----------: | :-----------:| :-----------: | :----------:| :----------:|
| ethanol      |  ethanol | CH<sub>3</sub>CH<sub>2</sub>OH | ![](images/ethanol.png) | CCO|
| acetic acid   | ethanoic acid | CH<sub>3</sub>COOH  |![](images/acetic_acid.png)| CC(=O)O |
|cyclohexane | cyclohexane | C<sub>6</sub>H<sub>12</sub>| ![](images/cyclohexane.png)  | C1CCCCC1 | 
| diphenylmethane | 1,1'-methylenedibenzene |(C<sub>6</sub>H<sub>5</sub>)<sub>2</sub>CH<sub>2</sub>|![](images/diphenylmethane.png)|C1=CC=C(C=C1)CC2=CC=CC=C2|

Perhaps the most important property of SMILES, as it relates to data science, is that the data is quite compact compared to other methods. For example, SMILES structures are around 1.6 bytes per atom, on average. This is quite small, especially when compared to standard skeletal image files, which have an averge size of 4.0 kilobytes.

## Question <a name="Question"></a>
Can I build a database of unique SMILES text targets, each corresponding to a unique element or molecule, and use those to obtain chemical names and images of each molecule?

## Data <a name="Data"></a>
I used a combination of sources to get my data, starting with [eMolecules](https://www.emolecules.com) for the unique SMILES strings followed by querying [PubChem](https://pubchem.ncbi.nlm.nih.gov/) for skeletal formulas and IUPAC names. 

### Cleaning the SMILES Data  <a name="smiles_data"></a>
This data was available to download for free, and contained 22,327,838 unique SMILES strings.

**Table 3**: Example rows from SMILES data

| isosmiles      | version_id | parent_id | 
| :-----------: | :-----------:| :-----------: |
| c1ccccc1      |  479848 | 479848 |
| Cc1ccccc1C      |  299961464 | 299961464 |
| CCc1ccccc1      |  475202 | 475202 |
| BB      |  987804	 | 987804|
| [W]      |  481713 | 481713 |

Since my goal was to have a dataset of only hydrocarbons (compounds containing only hydrogen and carbon), I began by investigating the frequency of each element in the dataset. Since the frequency of elements in the SMILES dataset is correlated to the actual abundance of compounds containing each element, I expected carbon and hydrogen to be the most abundant elements. 

Looking at the frequency of each element and symbol in the data, this assumption was correct. Since the scale varied from 1000 to 1.75 x 10<sup>8</sup>, I broke down the frequency into two graphs.

![](images/more_frequent_symbols.png)

**Figure 1**: Frequency of the most abundant elements and symbols

It is indeed true that the elements corresponding to organic molecules are the most abundant, with carbon (C and c), hydrogen (H), nitrogen (N) and oxygen (O) occuring in almost every compound.

![](images/less_frequent_symbols.png)

**Figure 2**: Frequency of the rarer elements and symbols

On the low end are rare elements, such as elemental tungsten. 

After learning what the data looks like, I removed all rows containing elements other than hydrogen and carbon. Doing so shrunk my dataset down to a more manageable 2,135 rows.

### Matching SMILES Strings to Skeletal Formulas <a name="skeletal_images"></a>

With my hydrocarbon dataset, I was now able to query [PubChem](https://pubchem.ncbi.nlm.nih.gov/) for the skeletal formulas. The URLs containing each image are easy to generate, as they all follow the same format. Each URL generated a .png image file of each molecule, which I downloaded and added to the dataset.

| SMILES      | Image URL | Skeletal Formula | 
| :-----------: |:-----------: | :-----------: |
|C=CCC1(CC=C)c2ccccc2-c2ccccc12| https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/smiles/C=CCC1(CC=C)c2ccccc2-c2ccccc12/PNG | ![](images/313754005.png)|
|Cc1ccc(C=C)c2ccccc12| https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/smiles/Cc1ccc(C=C)c2ccccc12/PNG |![](images/313870557.png)|
|Cc1ccccc1\C=C\c1ccccc1	|  https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/smiles/Cc1ccccc1\C=C\c1ccccc1/PNG | ![](images/32717.png)| 

### Matching SMILES Strings to IUPAC Names <a name="iupac_names"></a>

Names of each compound were also available on [PubChem](https://pubchem.ncbi.nlm.nih.gov/), stored in .json 

| SMILES      | JSON URL | IUPAC Preffered Name | 
| :-----------: |:-----------: | :-----------: |
|C=CCC1(CC=C)c2ccccc2-c2ccccc12| https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/smiles/C=CCC1(CC=C)c2ccccc2-c2ccccc12/JSON |9,9-bis(prop-2-enyl)fluorene |
|Cc1ccc(C=C)c2ccccc12| https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/smiles/Cc1ccc(C=C)c2ccccc12/JSON | 1-ethenyl-4-methylnaphthalene|
|Cc1ccccc1\C=C\c1ccccc1	|  https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/smiles/Cc1ccccc1\C=C\c1ccccc1/JSON | 1-methyl-2-[(E)-2-phenylethenyl]benzene

Parsing the JSON in the above links has given me more metadata than I intended to gather. The completed dataset has up to 1,342 separate attributes for each molecule. 

## Future Work <a name="future_work"></a>

In order to have a dataset that is usable to model a wide variety of molecules, I will need to expand the dataset to include chemical species other than hydrocarbons. Scaling up to cleaning and matching 23 million compounds with their images and names will need to be done on an AWS instance using Spark.

Furthermore, the above methodology of generating links does not work for some SMILES strings. For example, strings with triple bonds (designated with a #) break the URL strings and return 400 errors. Any large scale querying will need to be through the [PubChem PUG REST API ](https://pubchemdocs.ncbi.nlm.nih.gov/pug-rest). 
