# Building a scalable database of chemical names and structures from simplified molecular-input line-entry system (SMILES) strings 
## Carly Wolfbrandt

### Table of contents
1. [Introduction](#Introduction)
    1. [SMILES](#SMILES)
    2. [Skeletal Formulae](#skeletal_formulae)
2. [Background](#Background)
3. [Question](#Question)
4. [Data](#Data)
    1. [SMILES Data](#smiles_data)
    2. [Skeletal Images](#skeletal_images)
    3. [metadata](#metadata)

## Introduction <a name="Introduction"></a>

### Skeletal Formulae <a name="skeletal_formulae"></a>

The skeletal formula of a chemical species is a type of molecular structural formula that serves as a shorthand representation of a molecule's bonding and contains some information about its molecular geometry. It is represented in two dimensions, and is usually hand-drawn as a shorthand representation for sketching species or reactions. This shorthand representation is particularly useful in that carbons and hydrogens, the two most common atoms in organic chemistry, don't need to be explicitly drawn. These structural formulas contain the same information that the SMILES strings contain, but are depicted in a different way.

**Table 1**: Examples of different chemical species' names, molecular formulae and skeletal formulae

| Common Name      | IUPAC Name |Molecular Formula | Skeletal Formula | 
| :-----------: | :-----------:| :-----------: | :----------:| 
| ethanol      |  ethanol | CH<sub>3</sub>CH<sub>2</sub>OH | ![](/ethanol.png) |
| acetic acid   | ethanoic acid | CH<sub>3</sub>COOH  |![](/acetic_acid.png)|
|benzene | cyclo-hex-1,3,5-triene | C<sub>6</sub>H<sub>6</sub> |![](/benzene.jpg)  |
|cyclohexane | cyclohexane | C<sub>6</sub>H<sub>12</sub>| ![](/cyclohexane.png)  |
| diphenylmethane | 1,1'-methylenedibenzene | (C<sub>6</sub>H<sub>5</sub>)<sub>2</sub>CH<sub>2</sub>|![](/diphenylmethane.png)|



### Simplified Molecular-Input Line-Entry System (SMILES) <a name="SMILES"></a>

SMILES is a line notation for describing the structure of chemical elements or compounds using short ASCII strings. These strings can be thought of as a language, where atoms and bond symbols make up the vocabulary. 

SMILES formulae use atoms and bond symbols to describe physical properties of chemical species in the same way that a drawing of the structure conveys information about elements and bonding orientation. This means that the SMILES string for each molecule is synonymous with its structure and since the strings are unique, the name is universal. Anyone in the world who uses unique SMILES to name a molecule will choose the exact same name. These strings can be imported by most molecule editors for conversion into other chemical representations, including structural drawings and spectral predictions. 


**Table 2**: SMILES strings contrasted with skeletal formulae

| Common Name      | IUPAC Name |Molecular Formula | Skeletal Formula |  SMILES String |
| :-----------: | :-----------:| :-----------: | :----------:| :----------:|
| ethanol      |  ethanol | CH<sub>3</sub>CH<sub>2</sub>OH | ![](/ethanol.png) | CCO|
| acetic acid   | ethanoic acid | CH<sub>3</sub>COOH  |![](/acetic_acid.png)| CC(=O)O |
|benzene | cyclo-hex-1,3,5-triene | C<sub>6</sub>H<sub>6</sub> |![](/benzene.jpg)  | c1ccccc1  |
|cyclohexane | cyclohexane | C<sub>6</sub>H<sub>12</sub>| ![](/cyclohexane.png)  | C1CCCCC1 | 
| diphenylmethane | 1,1'-methylenedibenzene |(C<sub>6</sub>H<sub>5</sub>)<sub>2</sub>CH<sub>2</sub>|![](/diphenylmethane.png)|C1=CC=C(C=C1)CC2=CC=CC=C2|

Perhaps the most important property of SMILES, as it relates to data science, is that the data is quite compact compared to other methods. For example, SMILES structures are around 1.6 bytes per atom, on average. This is quite small, especially when compared to standard skeletal image files, which have an averge size of 4.0 kilobytes.

## Background <a name="Background"></a>
“Is there a Crisis in Organic Chemistry Education?” This provocatively titled session from the 2016 American Chemical Society national meeting drew attention from many in attendance. In fact, this question continues to be a polarizing topic of conversation in chemical education. 
 
On one side are those who work in academic publishing, who believe that the wealth of textbooks, electronic study guides, and databases with tens of thousands of questions mean that students are able to learn more quickly and more thoroughly. 
 
On the other side are educators, who assert that there is so much information to be learned, it is akin to drinking from a firehose. This fast pace leaves students feeling overwhelmed, and forces them into memorization mode. In fact, research about how students learn supports this stance. James Stigler, a UCLA professor who has been studying this crisis of memorization since the 1970’s, has shown that American students think learning math and science is about memorizing procedures. “They're not learning in a deep way… Students need practice in the things they can't learn by doing a Google search.”
 
How do we lighten the load of the traditional organic chemistry curriculum so students have time to practice problems that can’t be learned through a Google search?  We can begin by unburdening students with needless memorization, and thus leave more time and mental resources for deep learning. A quick Google search of “what to memorize for organic chemistry” shows that, while many educators agree that a deep understanding is not achieved through memorization, there are some things that “just need to be memorized.” At the top of almost every “need to memorize” list is how to name chemical structures. How do we alleviate the need to memorize these naming conventions, and thus eliminate weeks of lectures and homework in a traditional organic chemistry curriculum? 
 
Machine learning of course! An image captioning model for organic chemical structures using a stacked CNN-LSTM would make it possible to get the name of any known chemical structure just from an image. This is a particularly attractive solution, since nearly every student has a phone in their pocket with a camera on them at all times. No need to draw the structure using bulky software and upload the image into an unintuitive online portal, just take a photo of the structure in question and pass it through the model. By removing memorization of naming conventions from the curriculum, students could shift their focus to novel problems that can’t be solved through a quick Google search.

## Question <a name="Question"></a>
Can I build a database of unique SMILES text targets, each corresponding to a unique element or molecule, and use those to obtain chemical names and images of each molecule?



## Data <a name="Data"></a>
The first paragraph text

### Sub paragraph <a name="subparagraph1"></a>
This is a sub paragraph, formatted in heading 3 style

## Another paragraph <a name="paragraph2"></a>
The second paragraph text
