<!-- README.md is generated from README.Rmd. Please edit that file -->
![PGRdup](inst/extdata/PGRdup.svg) \#\# PGRdup: Methods to Aid Identification of Probable Duplicates in PGR Passport Databases \#\#\#\#\# *J. Aravind, J. Radhamani, Kalyani Srinivasan, B. Ananda Subhash and R. K. Tyagi* \#\#\#\#\#\# Copyright (C) 2014, [ICAR-NBPGR](http://www.nbpgr.ernet.in/) ; License: [GPL-2 | GPL-3](http://www.r-project.org/Licenses/)

The `R` package `PGRdup` was developed as a tool to aid genebank managers in the identification of probable duplicate accessions from plant genetic resources (PGR) passport databases.

This package primarily implements a workflow designed to fetch groups or sets of germplasm accessions with similar passport data particularly in fields associated with accession names within or across PGR passport databases.

The functions in this package are primarily built using the following R packages: \* [`data.table`](http://cran.r-project.org/web/packages/data.table/index.html) \* [`igraph`](http://cran.r-project.org/web/packages/igraph/index.html) \* [`stringdist`](http://cran.r-project.org/web/packages/stringdist/index.html) \* [`stringi`](http://cran.r-project.org/web/packages/stringi/index.html)

Workflow
--------

The series of steps involve in the workflow along with the associated functions are are illustrated below: \#\#\#\# Step 1 **Function(s) :** \* `DataClean` \* `MergeKW` \* `MergePrefix` \* `MergeSuffix`

Use these functions for the appropriate data standardisation of the relevant fields in the passport databases to harmonize punctuation, leading zeros, prefixes, suffixes etc. associated with accession names.

#### Step 2

**Function(s) :** \* `KWIC`

Use this function to extract the information in the relevant fields as keywords or text strings in the form of a searchable Keyword in Context (KWIC) index.

#### Step 3

**Function(s) :** \* `ProbDup`

Execute fuzzy, phonetic and semantic matching of keywords to identify probable duplicate sets either within a single KWIC index or between two indexes using this function. For fuzzy matching the levenshtein edit distance is used, while for phonetic matching, the double metaphone algorithm is used. For semantic matching, synonym sets or ‘synsets’ of accession names can be supplied as an input and the text strings in such sets will be treated as being identical for matching. Various options to tweak the matching strategies used are also available in this function.

#### Step 4

**Function(s) :** \* `DisProbDup` \* `ReviewProbDup` \* `ReconstructProbDup`

Inspect, revise and improve the retrieved sets using these functions. If considerable intersections exist between the initially identified sets, then `DisProbDup` may be used to get the disjoint sets. The identified sets may be subjected to clerical review after transforming them into an appropriate spreadsheet format which contains the raw data from the original database(s) using `ReviewProbDup` and subsequently converted back using `ReconstructProbDup`.

#### Adjuncts

**Function(s) :** \* `ValidatePrimKey` \* `DoubleMetaphone` \* `ParseProbDup` \* `AddProbDup`

Use these helper functions if needed. `ValidatePrimKey` can be used to check whether a column chosen in a data.frame as the primary primary key/ID confirms to the constraints of absence of duplicates and NULL values. `DoubleMetaphone` is an implementation of the Double Metaphone phonetic algorithm in `R` and is used for phonetic matching. `ParseProbDup` and `AddProbDup` work with objects of class `ProbDup`. The former can be used to parse the probable duplicate sets in a `ProbDup` object to a `data.frame` while the latter can be used to add these sets data fields to the passport databases.

Tips
----

-   Use [`fread`](http://www.rdocumentation.org/packages/data.table/functions/fread) to rapidly read large files instead of `read.csv` or `read.table` in `base`.
-   In case the PGR passport data is in any DBMS, use the appropriate [`R`-database interface packages](http://www.burns-stat.com/r-database-interfaces/) to get the required table as a `data.frame` in `R`.

Note
----

-   The `ProbDup` function can be memory hungry with large passport databases. In such cases, ensure that the system has sufficient memory for smooth functioning (See `?ProbDup`).
