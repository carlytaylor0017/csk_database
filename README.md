{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Building a scalable database of chemical names and structures from simplified molecular input line entry system (SMILES) strings \n",
    "## Carly Wolfbrandt\n",
    "### Data from: Pubchem, eMolecules"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Table of contents\n",
    "1. [Introduction](#Introduction)\n",
    "    1. [Question](#Question)\n",
    "    2. [Background](#Background)\n",
    "    3. [SMILES](#SMILES)\n",
    "2. [Data](#Data)\n",
    "    1. [Sub paragraph](#subparagraph1)\n",
    "3. [Another paragraph](#paragraph2)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Introduction <a name=\"Introduction\"></a>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Question <a name=\"Question\"></a>\n",
    "Can I build a database of unique SMILES text targets, each corresponding to a unique element or molecule, and use those to obtain chemical names and images of each molecule?"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Background <a name=\"Background\"></a>\n",
    "\n",
    "“Is there a Crisis in Organic Chemistry Education?” This provocatively titled session from the 2016 American Chemical Society national meeting drew attention from many in attendance. In fact, this question continues to be a polarizing topic of conversation in chemical education. \n",
    " \n",
    "On one side are those who work in academic publishing, who believe that the wealth of textbooks, electronic study guides, and databases with tens of thousands of questions mean that students are able to learn more quickly and more thoroughly. \n",
    " \n",
    "On the other side are educators, who assert that there is so much information to be learned, it is akin to drinking from a firehose. This fast pace leaves students feeling overwhelmed, and forces them into memorization mode. In fact, research about how students learn supports this stance. James Stigler, a UCLA professor who has been studying this crisis of memorization since the 1970’s, has shown that American students think learning math and science is about memorizing procedures. “They're not learning in a deep way… Students need practice in the things they can't learn by doing a Google search.”\n",
    " \n",
    "How do we lighten the load of the traditional organic chemistry curriculum so students have time to practice problems that can’t be learned through a Google search?  We can begin by unburdening students with needless memorization, and thus leave more time and mental resources for deep learning. A quick Google search of “what to memorize for organic chemistry” shows that, while many educators agree that a deep understanding is not achieved through memorization, there are some things that “just need to be memorized.” At the top of almost every “need to memorize” list is how to name chemical structures. How do we alleviate the need to memorize these naming conventions, and thus eliminate weeks of lectures and homework in a traditional organic chemistry curriculum? \n",
    " \n",
    "Machine learning of course! An image captioning model for organic chemical structures using a stacked CNN-LSTM would make it possible to get the name of any known chemical structure just from an image. This is a particularly attractive solution, since nearly every student has a phone in their pocket with a camera on them at all times. No need to draw the structure using bulky software and upload the image into an unintuitive online portal, just take a photo of the structure in question and pass it through the model. By removing memorization of naming conventions from the curriculum, students could shift their focus to novel problems that can’t be solved through a quick Google search.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### SMILES <a name=\"SMILES\"></a>\n",
    "\n",
    "SMILES contains the same information as might be found in an extended connection table. The primary reason SMILES is more useful than a connection table is that it is a linguistic construct, rather than a computer data structure. SMILES is a true language, albeit with a simple vocabulary (atom and bond symbols) and only a few grammar rules. SMILES representations of structure can in turn be used as \"words\" in the vocabulary of other languages designed for storage of chemical information (information about chemicals) and chemical intelligence (information about chemistry).\n",
    "\n",
    "| Name      | SMILES String | Molecular Formula |\n",
    "| :-----------: | :-----------: | :----------:|\n",
    "| ethanol      | CCO       | CH<sub>3</sub>CH<sub>2</sub>OH |\n",
    "| acetic acid   | CC(=O)O | CH<sub>3</sub>COOH |\n",
    "\n",
    "Part of the power of SMILES is that unique SMILES exist. With standard SMILES, the name of a molecule is synonymous with its structure; with unique SMILES, the name is universal. Anyone in the world who uses unique SMILES to name a molecule will choose the exact same name.\n",
    "\n",
    "One other important property of SMILES is that it is quite compact compared to most other methods of representing structure. A typical SMILES will take 50% to 70% less space than an equivalent connection table, even binary connection tables. For example, a database of 23,137 structures, with an average of 20 atoms per structure, uses only 1.6 bytes per atom when represented with SMILES. In addition, ordinary compression of SMILES is extremely effective. The same database cited above was reduced to 27% of its original size by Ziv-Lempel compression (i.e. 0.42 bytes per atom)\n",
    "\n",
    "## Data <a name=\"Data\"></a>\n",
    "The first paragraph text\n",
    "\n",
    "### Sub paragraph <a name=\"subparagraph1\"></a>\n",
    "This is a sub paragraph, formatted in heading 3 style\n",
    "\n",
    "## Another paragraph <a name=\"paragraph2\"></a>\n",
    "The second paragraph text"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
