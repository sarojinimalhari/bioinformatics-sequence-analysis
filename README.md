# bioinformatics-sequence-analysis
Sequence alignment

I ran an in silico protein analysis to identify an uncharacterized 246-amino-acid sequence and explore its structural features. Using NCBI’s BLASTP, I mapped the sequence against the human protein database to pinpoint its identity, check for evolutionary conservation, and see what functional domains it carries. 

**Step-by-Step WorkflowQuery Setup:** 

Inputted the raw 246 aa sequence (lcl|Query_9732341) into NCBI BLASTP. 
Database Selection: Filtered the search specifically against Homo sapiens using the ClusteredNR database to compare against curated human non-redundant protein clusters. 
Domain Search: Scanned for conserved domain architectures alongside the primary sequence alignment. 

**Key Findings & Alignment BreakdownTarget Identified:** 

The sequence is a 100% exact match for Breast Cancer Metastasis-Suppressor 1 (BRMS1), specifically isoform 2 (Accession: NP_001020128.1). 
**Statistical Significance:**
The alignment yielded an E-value of $2 \times 10^{-173}$ and a Bit Score of 481. In plain terms, an E-value this close to zero means there is essentially a 0% chance this sequence match happened by random coincidence.  
**Isoform Differences:**
Isoform X2 (XP_024304194.1) matched at 95.10% identity. Looking closely at the alignment tail, the divergence occurs right at the C-terminus (around residues 235–245), where X2 has a unique peptide extension (TGGPTGPSGSAQPG). 
**Functional Architecture:**
The graphical summary revealed an Sds3 (Sin3 histone deacetylase core complex component) superfamily domain spanning roughly residues 80 to 160.

Biological TakeawaysBRMS1 plays a heavy-hitting role in cancer research—it actively suppresses tumor metastasis (the spread of cancer to other organs) without necessarily stopping the primary tumor from growing. Discovering the Sds3 domain in this region highlights how BRMS1 binds into the mSin3-HDAC corepressor complex, helping regulate gene silencing and chromatin remodeling.

Figure 1: BLASTP search configuration in NCBI, running the 246 aa query against the human ClusteredNR database.
<img width="1167" height="847" alt="Screenshot 2026-08-25 215636" src="https://github.com/user-attachments/assets/f1b15171-8983-467b-8277-933518dad2ee" />

Figure 2: NCBI graphic summary showing uniform high-score hits across all three clusters and highlighting the conserved Sds3 superfamily domain (~residues 80–160).
<img width="1172" height="667" alt="Screenshot 2026-08-25 221219" src="https://github.com/user-attachments/assets/04180522-85ce-46d1-bdee-fb06340382f8" />


**Raw BLAST Output**

Here is the exact output file exported from NCBI BLAST for reference and verification:

Program: BLASTP 
Query: unnamed protein product ID: lcl|Query_9732341(amino acid) Length: 246
Database: ClusteredNR clustered nr

Clusters producing significant alignments:
Cluster Rep.: breast cancer metastasis-suppressor 1 isoform 2 [Homo sapiens]
Accession: NP_001020128.1 | Max Score: 481 | Query Cover: 99% | E-value: 2e-173 | Identity: 100.00%

>breast cancer metastasis-suppressor 1 isoform 2 [Homo sapiens]
Sequence ID: NP_001020128.1 Length: 290
Range 1: 1 to 244

Score:481 bits(1237), Expect:2e-173, 
Method:Compositional matrix adjust., 
Identities:244/244(100%), Positives:244/244(100%), Gaps:0/244(0%)

Query  1    MPVQPPSKDTEEMEAEGDSAAEMNGEEEESEEERSGSQTESEEESSEMDDEDYERRRSEC  60
            MPVQPPSKDTEEMEAEGDSAAEMNGEEEESEEERSGSQTESEEESSEMDDEDYERRRSEC
Sbjct  1    MPVQPPSKDTEEMEAEGDSAAEMNGEEEESEEERSGSQTESEEESSEMDDEDYERRRSEC  60

Query  61   VSEMLDLEKQFSELKEKLFRERLSQLRLRLEEVGAERAPEYTEPLGGLQRSLKIRIQVAG  120
            VSEMLDLEKQFSELKEKLFRERLSQLRLRLEEVGAERAPEYTEPLGGLQRSLKIRIQVAG
Sbjct  61   VSEMLDLEKQFSELKEKLFRERLSQLRLRLEEVGAERAPEYTEPLGGLQRSLKIRIQVAG  120

Query  121  IYKGFCLDVIRNKYECELQGAKQHLESEKLLLYDTLQGELQERIQRLEEDRQSLDLSSEW  180
            IYKGFCLDVIRNKYECELQGAKQHLESEKLLLYDTLQGELQERIQRLEEDRQSLDLSSEW
Sbjct  121  IYKGFCLDVIRNKYECELQGAKQHLESEKLLLYDTLQGELQERIQRLEEDRQSLDLSSEW  180

Query  181  WDDKLHARGSSRSWDSLPPSKRKKAPLVSGPYIVYMLQEIDILEDWTAIKKARAAVSPQK  240
            WDDKLHARGSSRSWDSLPPSKRKKAPLVSGPYIVYMLQEIDILEDWTAIKKARAAVSPQK
Sbjct  181  WDDKLHARGSSRSWDSLPPSKRKKAPLVSGPYIVYMLQEIDILEDWTAIKKARAAVSPQK  240

Query  241  RKSD  244
            RKSD
Sbjct  241  RKSD  244

**Summary**

Overall, this alignment confirms the sequence is human BRMS1 isoform 2. Identifying the Sds3 domain confirms its role in chromatin remodeling and helping stop cancer cells from spreading.


: Protein Structure Prediction — Human BRCA1

## Overview
For this task, I worked on predicting and studying the 3D structure of the human BRCA1 protein using AlphaFold. Since I had already done Task 1 on human breast cancer, I wanted to keep working in the same area, so I picked BRCA1 — it's probably the single most well-known gene/protein connected to breast cancer, and I was curious to actually see what it looks like in 3D instead of just reading about it.

The main idea behind this task was simple: take a protein sequence, predict its structure, and then actually look at that structure to understand something about how the protein works.

## Introduction
BRCA1 stands for "Breast Cancer type 1 susceptibility protein." Most people have heard of it because of the BRCA1/BRCA2 gene tests that are used to check a person's risk of breast and ovarian cancer. What BRCA1 actually does inside the cell is help repair damaged DNA. Every cell in our body deals with small amounts of DNA damage all the time, and there are proteins whose whole job is to fix that damage before it causes problems. BRCA1 is one of the key players in this repair process.

When BRCA1 is mutated, this repair system doesn't work properly anymore. Damaged DNA starts piling up in cells instead of getting fixed, and over time that damage can lead to the kind of uncontrolled changes that cause cancer. That's the whole reason BRCA1 mutations are associated with a much higher risk of breast and ovarian cancer.

Here's something interesting I learned while doing this task: scientists have never been able to experimentally solve the complete 3D structure of BRCA1 in a lab. It's a huge protein (1863 amino acids), and only small fragments of it — like the very beginning and the very end — have ever been captured experimentally. This is exactly the kind of situation where AI-based structure prediction is genuinely useful, instead of just being a shortcut. AlphaFold, developed by Google DeepMind, predicts what a protein's 3D shape probably looks like, based only on its amino acid sequence, using a model trained on thousands of known protein structures.

**Protein studied:** BRCA1_HUMAN (Breast cancer type 1 susceptibility protein)
**UniProt ID:** P38398
**Organism:** Homo sapiens (human)
**Sequence length:** 1863 amino acids
**Source database:** AlphaFold Protein Structure Database (AlphaFold DB)

## Methodology
I followed a fairly straightforward process for this task:

**Step 1 — Getting the sequence from UniProt.**
I went to UniProt.org and searched for BRCA1 human. This brought up the reviewed entry P38398 (BRCA1_HUMAN), which confirmed the protein is 1863 amino acids long and gave me background on its known function — mainly its role as an E3 ubiquitin ligase involved in DNA damage repair.

**Step 2 — Finding the predicted structure on AlphaFold DB.**
Next, I went to the AlphaFold Protein Structure Database and searched for P38398. One thing I ran into here is that AlphaFold DB can show different isoforms of the same protein, and at first I accidentally opened isoform 2 (`AF-P38398-2-F1`), which turned out to be a much shorter fragment (only around 63 amino acids) rather than the full protein. After noticing the sequence length didn't match, I went back and made sure I opened the correct canonical entry, `AF-P38398-F1`, which covers the full 1863-residue protein.

**Step 3 — Visualizing the structure.**
AlphaFold DB has a built-in 3D viewer (Mol*) that I used to actually look at the structure. I viewed it in two different ways:
- Colored by **pLDDT confidence score** — this shows, region by region, how confident the AI model is about that part of the predicted shape.
- Colored by **secondary structure** — this shows where the helices, beta-strands, and loops are.

**Step 4 — Zooming into specific regions.**
Rather than just looking at the whole protein from far away, I zoomed into two regions that are known to be functionally important:
- The **RING domain**, near the very start of the protein (roughly residues 1–100).
- The **BRCT domains**, near the very end of the protein (roughly residues 1650–1863).

For each of these, I took screenshots to document what I found.

## Results
**Whole-structure view:**
When I looked at the full-length structure colored by confidence, the pattern was pretty clear: there are two compact, tightly folded regions — one near the start and one near the end — and in between them, a very long stretch of chain that doesn't fold into any clear shape at all. In the confidence coloring, the folded ends showed up blue (high confidence), while the long middle stretch was mostly yellow and orange (low confidence).

At first I thought the low confidence in the middle might just mean AlphaFold "wasn't sure," but this actually matches what's known biologically — that middle section of BRCA1 is genuinely an intrinsically disordered region. It doesn't have one fixed shape in real life either, so the low confidence score isn't really a mistake in the prediction; it's the model correctly picking up on the fact that this part of the protein doesn't have a stable structure to predict in the first place.

**RING domain (residues ~1–100):**
This region folds into a small, compact structure made of a helix packed together with a couple of beta-strands. This is the part of BRCA1 that lets it act as an enzyme — specifically, it works together with another protein called BARD1 to tag other proteins with a small molecular marker (ubiquitin), which is one of the signals that gets DNA repair pathways going.

**BRCT domains (residues ~1650–1863):**
Near the very end of the protein, there are two similarly-shaped folded regions sitting close together — these are called the tandem BRCT domains. Their job is to recognize and bind to other proteins that have been tagged with a phosphate group after DNA damage occurs, which is basically how BRCA1 gets "recruited" to the site of damage in the first place.

**Figure 1:** UniProt entry page (P38398 · BRCA1_HUMAN) detailing the biological role, primary sequence length (1863 amino acids), and catalytic E3 ubiquitin-protein ligase activity.
<img width="1917" height="805" alt="Screenshot 2026-09-04 200103" src="https://github.com/user-attachments/assets/bedb7cea-44c0-43e9-96a4-2a73bbe5fb60" />

**Figure 2:** AlphaFold Structure Database summary for BRCA1 (AF-P38398-2-F1), displaying overall pLDDT model confidence scores and metadata.
<img width="1895" height="681" alt="Screenshot 2026-09-04 200128" src="https://github.com/user-attachments/assets/d3b87ff6-ce5d-4b31-8a5c-ff2a6efc22aa" />

**Figure 3:** 3D ribbon rendering of the complete BRCA1 protein monomer color-mapped by per-residue pLDDT confidence scores (high confidence in dark blue, lower confidence in yellow/orange).
<img width="1912" height="821" alt="Screenshot 2026-09-04 202404" src="https://github.com/user-attachments/assets/04431fb8-6993-4260-977c-48c0e4402ed6" />

**Figure 4:** Close-up 3D cartoon representation showing specific secondary structure motifs (alpha-helices in magenta, beta-strands in yellow, and loops in green).
<img width="1024" height="525" alt="image" src="https://github.com/user-attachments/assets/12223c4f-99ed-4ecb-843c-092764690eb4" />

**Figure 5:** Ball-and-stick view showing explicit side-chain coordinates, hydrogen bonding (blue dashes), and non-covalent interactions centered on a highlighted amino acid.
<img width="1024" height="589" alt="image" src="https://github.com/user-attachments/assets/87f1ad38-d7f8-46c0-b28a-065434e105b7" />

**Figure 6:** High-magnification structural panel displaying hydrogen bonding networks and spatial orientation of side chains near residues 1650–1863.
<img width="1024" height="541" alt="image" src="https://github.com/user-attachments/assets/919d8ffd-af98-496e-9786-df523ea641e1" />

**Raw Data Output**

[AF-P38398-2-F1-model_v6.pdb](https://github.com/user-attachments/files/31848781/AF-P38398-2-F1-model_v6.pdb)


## Conclusion
Doing this task made it a lot clearer to me why BRCA1 mutations are so strongly tied to breast cancer risk. The protein's structure basically has two small, precisely-folded "working parts" — the RING domain and the BRCT domains — connected by a long, floppy middle section that doesn't need a fixed shape to do its job. Almost all of BRCA1's actual biochemical work happens in those two folded ends.

That also explains something important: most of the cancer-linked mutations in BRCA1 that researchers have identified fall inside the RING domain or the BRCT domains, not in the long disordered middle. That makes sense once you've actually seen the structure — damaging a small, precisely-folded region is much more likely to break its function completely, while the disordered middle can probably tolerate more change without losing much. Being able to visualize that, instead of just reading it as a fact, made the connection between structure and disease feel a lot more concrete.

---
**Tools used:** UniProt, AlphaFold Protein Structure Database (Mol* viewer)
**Task:** CodeAlpha Bioinformatics Internship — Task 3 (Protein Structure Prediction)






