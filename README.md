# bioinformatics-sequence-analysis
Sequence alignment
I ran an in silico protein analysis to identify an uncharacterized 246-amino-acid sequence and explore its structural features. Using NCBI’s BLASTP, I mapped the sequence against the human protein database to pinpoint its identity, check for evolutionary conservation, and see what functional domains it carries. 

Step-by-Step WorkflowQuery Setup: 
Inputted the raw 246 aa sequence (lcl|Query_9732341) into NCBI BLASTP. 
Database Selection: Filtered the search specifically against Homo sapiens using the ClusteredNR database to compare against curated human non-redundant protein clusters. 
Domain Search: Scanned for conserved domain architectures alongside the primary sequence alignment. 

Key Findings & Alignment BreakdownTarget Identified: 
The sequence is a 100% exact match for Breast Cancer Metastasis-Suppressor 1 (BRMS1), specifically isoform 2 (Accession: NP_001020128.1). 
Statistical Significance: The alignment yielded an E-value of $2 \times 10^{-173}$ and a Bit Score of 481. In plain terms, an E-value this close to zero means there is essentially a 0% chance this sequence match happened by random coincidence.  
Isoform Differences: Isoform X2 (XP_024304194.1) matched at 95.10% identity. Looking closely at the alignment tail, the divergence occurs right at the C-terminus (around residues 235–245), where X2 has a unique peptide extension (TGGPTGPSGSAQPG). 
Functional Architecture: The graphical summary revealed an Sds3 (Sin3 histone deacetylase core complex component) superfamily domain spanning roughly residues 80 to 160.

Biological TakeawaysBRMS1 plays a heavy-hitting role in cancer research—it actively suppresses tumor metastasis (the spread of cancer to other organs) without necessarily stopping the primary tumor from growing. Discovering the Sds3 domain in this region highlights how BRMS1 binds into the mSin3-HDAC corepressor complex, helping regulate gene silencing and chromatin remodeling.
