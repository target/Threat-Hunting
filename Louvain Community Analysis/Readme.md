## Threat Hunting - Louvain Community Analysis
In this folder you will find notebooks that use the Louvain community analysis algorithm on a graph made from arbitrary tabular data, and returns any communities with 
statistically small sizes.  This is useful in identifying rare relationships between columns, which can help threat hunters reduce large data sets into much smaller
subsets that may warrant further investigation.

Source: https://python-louvain.readthedocs.io/en/latest/api.html

### louvain_community_analyzer
Uses the Python-Louvain module to find the rarest commmunities identified within an undirected graph network.
Begin by building a CSV file of any data you'd like.  Reduce it to only the columns you are most interested in.  The code will then build an undirected
NetworkX graph from the columns, and then apply the Louvain analysis to identify the rarest communities from within the graph.  Upload the 
CSV file to the same path your notebook runs from.

Prerequisite: Jupyter Notebook (https://jupyter.org/install)
