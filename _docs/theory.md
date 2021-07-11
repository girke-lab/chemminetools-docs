---
title: "Theory: Descriptors, Similarity Measures, and Clustering Schemes"
permalink: /docs/theory/
---

## Introduction

This section provides a brief overview of the cheminformatics and clustering algorithms used by ChemMine Tools. At the beginning of each subsection the services are listed in brackets [] where the corresponding methods and algorithms are used.

## Structure Similarity Comparisons and Searching of Small Molecules

To compare, cluster and search small molecules with respect to their structural similarities, a common approach is to enumerate their structural features, which are often referred to as structural descriptors. The numbers of common and unique features are then used to calculate a similarity measure among two compounds. The descriptor types and similarity coefficients used by ChemMine Tools are described below.

### Structural Descriptors

#### 1. Structural Descriptors
  
##### a. Atom Pairs &nbsp; &nbsp; [   [Similarity Comparison](https://chemminetools.ucr.edu/similarity/)  &nbsp; &nbsp;  [Clustering](https://chemminetools.ucr.edu/myCompounds/addCompoundsNoneNone)   ]
  
Atom pairs are a structural descriptor type that is defined by the shortest paths among the non-hydrogen atoms in a molecule. Each path is described by the types of atoms in a pair, the length of their shortest bond path, the number of their pi electrons and the non-hydrogen atoms bonded to them. The number of atom pairs describing a molecule grows with its number of atoms. To use atom pairs for similarity comparisons, one can simply enumerate their common and unique atom pairs, and then use these numbers to compute a similarity coefficient (see below).

##### (b.) PubChem Fingerprints &nbsp; [   Similarity Search   ]

The fingerprints provided by PubChem are a binary representation of the presence and absence of a library of 881 substructure features (see here for details). In this system every molecular structure is described by 881 bits where 1 indicates the presence and 0 the absence of a feature. Compared to atom pairs, the PubChem fingerprints are a knowledge-based system that stores less information than the much more complex and unbiased atom pair concept. For database searching fingerprints are often much more time and memory efficient, but they are less sensitive than atom pair descriptors (see Chen & Reynolds, 2002; Cao et al. 2008).

(c) Maximum Common Substructure
[   Similarity Comparison   ]
The maximum common substructure (MCS) problem is a graph-based similarity concept that is defined as the largest substructure (sub-graph) shared among two compounds. It is a pair-wise concept that is not directly related to the above structural descriptors, but its results (e.g. size of MCS relative to source structures) can be used for the computation of the same similarity coefficients (see below). Compared to descriptor-based similarity concepts, the MCS method provides the most accurate and sensitive similarity measure, especially for compounds with large size differences.

(2) Similarity Coefficients
(a) Tanimoto coefficient
[   Similarity Comparison   Similarity Search   Clustering   ]
The Tanimoto coefficient is defined as c/(a+b+c), which is the proportion of the features shared among two compounds divided by their union. The variable c is the number of features (or on-bits in binary fingerprint) common in both compounds, while a and b are the number of features that are unique in one or the other compound, respectively. The Tanimoto coefficient has a range from 0 to 1 with higher values indicating greater similarity than lower ones. It is important to emphasize that a Tanimoto coefficient of 1 does not necessarily mean that two compounds are identical. It only means that they have identical structural descriptors or identical on-bits in a binary fingerprint. To determine identity among two compounds, InChI strings usually provide a much more reliable solution. This latter feature will become available in ChemMine Tools soon.

(b) Tversky Index
[   Similarity Comparison   ]
The Tversky index is defined as c/(α*a + β*b + c). It extends the Tanimoto index by two weighting variables α and β. If α and β are set to 1 then the index returns the same result as the Tanimoto coefficient.

(c) Dice Index
[   Similarity Comparison   ]
Setting α and β in the Tversky index to 0.5 returns the Dice index.

Similarity Measures for Property and Activity Profiles
[   Clustering   ]
Sets of numeric property values of compounds, such as physiochemical properties or bioactivity values, can also be used to compute a similarity measure among compounds. For instance, ChemMine Tools uses the physiochemical descriptors of compounds - or any numeric custom data set - for the computation of Pearson correlation coefficients as similarity measure for the calculation of an item-to-item similarity matrix that can be converted into a distance matrix for downstream clustering.

Clustering based on property values is performed follows:

Scaling and centering the property table row-wise by subtracting from each value the row mean and then dividing by the standard deviation of each row.
Calculation of an all-against-all Pearson correlation matrix. This is transformed into a distance matrix by subtracting each value from 1.
Hierarchical clustering of this distance matrix.
Clustering Methods and Schemes
(a) Hierarchical Clustering
[   Clustering   ]
This services uses the hclust function implemented in R to perform hierarchical clustering. It requires as input a distance matrix of all-against-all compound distances that is generated by subtracting the similarity measure (e.g. Tanimoto coefficient Tc) from one (1 - Tc). The resulting distance matrix is then passed on to the actual clustering program that hierarchically joins the most to least similar items in an agglomerative manner using as cluster joining rule either single, average or complete linkage. The latter parameters are definable by the user.

(b) Multidimensional Scaling
[   Clustering   ]
Similar to hierarchical clustering, multidimensional scaling (MDS) starts with a matrix of item-item distances and then assign coordinates for each item in a low-dimensional space to represent the distances graphically in a scatter plot. The cmdscale function implemented in R is used for this service.

(c) Binning Clustering
[   Clustering   ]
Binning clustering assigns compounds to similarity groups based on a user-definable similarity cutoff. For instance, if a Tanimoto coefficient of 0.6 is chosen then compounds will be joined into groups that share a similarity of this value or greater using a single linkage rule for cluster joining. This method is based on an internally developed C++ implementation that is very memory efficient since it does not require a distance matrix as input. It calculates the required compound-to-compound distance information on the fly.
