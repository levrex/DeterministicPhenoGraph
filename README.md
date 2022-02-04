DeterministicPhenoGraph for Python3
======================

This is a deterministic implementation of PhenoGraph. It uses a consistent **seed** for the Louvain to ensure the results can be replicated. The PhenoGraph code was largely adopted from ["tfmodisco"](https://github.com/kundajelab/tfmodisco/))

[PhenoGraph](http://www.cell.com/cell/abstract/S0092-8674(15)00637-6) is a clustering method designed for high-dimensional single-cell data. It works by creating a graph ("network") representing phenotypic similarities between cells and then identifying communities in this graph.

This software package includes compiled binaries that run community detection based on C++ code written by E. Lefebvre and J.-L. Guillaume in 2008 (["Louvain method"](https://sites.google.com/site/findcommunities/)). The code has been altered to interface more efficiently with the Python code here. It should work on reasonably current Linux, Mac and Windows machines. 


To run basic clustering:

    from phenograph.cluster import cluster
    communities, graph, Q = cluster(data)

Another example:

    from phenograph.cluster import cluster
    communities, graph, Q = cluster(data, k=20, primary_metric='minkowski', n_jobs= 1)

For a dataset of *N* rows, `communities` will be a length *N* vector of integers specifying a community assignment for each row in the data. Any rows assigned `-1` were identified as *outliers* and should not be considered as a member of any community. `graph` is a *N* x *N* `scipy.sparse` matrix representing the weighted graph used for community detection.
`Q` is the modularity score for `communities` as applied to `graph`.

Disclaimer
-------------
- The leiden algorithm is not implemented in this version. 
- Multiprocessing doesn't work at the moment
- I want to add the possibility to change the seed as a user

Citation
-------------
If you use PhenoGraph in work you publish, please cite our publication:

    @article{Levine_PhenoGraph_2015,
      doi = {10.1016/j.cell.2015.05.047},
      url = {http://dx.doi.org/10.1016/j.cell.2015.05.047},
      year  = {2015},
      month = {jul},
      publisher = {Elsevier {BV}},
      volume = {162},
      number = {1},
      pages = {184--197},
      author = {Jacob H. Levine and Erin F. Simonds and Sean C. Bendall and Kara L. Davis and El-ad D. Amir and Michelle D. Tadmor and Oren Litvin and Harris G. Fienberg and Astraea Jager and Eli R. Zunder and Rachel Finck and Amanda L. Gedman and Ina Radtke and James R. Downing and Dana Pe'er and Garry P. Nolan},
      title = {Data-Driven Phenotypic Dissection of {AML} Reveals Progenitor-like Cells that Correlate with Prognosis},
      journal = {Cell}
    }

