# External metadata

| Name                                  | Description                          | Source                                                                                                                                     |
|:--------------------------------------|:-------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------|
| `JUMP-Target-1_compound_metadata.tsv` | Metadata for JUMP-Target-1 compounds | [link](https://github.com/jump-cellpainting/JUMP-Target/blob/0395c0060dcacde0dcd94c5c9c2199f867e86a87/JUMP-Target-1_compound_metadata.tsv) |
| `JUMP-Target-2_compound_metadata.tsv` | Metadata for JUMP-Target-2 compounds | [link](https://github.com/jump-cellpainting/JUMP-Target/blob/0395c0060dcacde0dcd94c5c9c2199f867e86a87/JUMP-Target-2_compound_metadata.tsv) |
| `orf_metadata.tsv`                    | Metadata for ORFs                    | [link](https://docs.google.com/spreadsheets/d/1X5DN3b5naGhllyZNnNA9rIsIeu0D7--9dAWbFAV_6pQ/edit#gid=1141482821)                            |

## Metadata description

See <https://github.com/jump-cellpainting/JUMP-Target> for `JUMP-Target-1_compound_metadata.tsv` and `JUMP-Target-2_compound_metadata.tsv`.

For `orf_metadata.tsv`:

| Column             | Description                                     |
|--------------------|-------------------------------------------------|
| Name               | Internal ID of ORF                              |
| Public ID          | Public ID of ORF                                |
| Vector             | ORF expression vector                           |
| Transcript         | NCBI reference sequence                         |
| Symbol             | NCBI gene symbol                                |
| NCBI Gene ID       | NCBI gene ID                                    |
| Taxon ID           | NCBI taxonomy ID                                |
| Gene Description   | Gene description                                |
| Annot. Gene Symbol | Annotation provided by source: NCBI gene symbol |
| Annot. Gene ID     | Annotation provided by source: NCBI gene ID     |
| Prot Match %       | % match to protein sequence                     |
| Insert Length      | Length of the ORF sequence                      |

<details>

Email snippets about the source of `orf_metadata.tsv` ([link](https://docs.google.com/spreadsheets/d/1X5DN3b5naGhllyZNnNA9rIsIeu0D7--9dAWbFAV_6pQ/edit#gid=1141482821)).

Note: this file was also copied over to [an internal repo](https://github.com/jump-cellpainting/jump-cellpainting/blob/4bd145565ebd6c91bc93e11d7456cc3086512ca8/7.design-orf-experiment/data/pLX_304_ORF_collection.csv).

---
  
For 577 rows, `Annot. Gene Symbol` != Symbol, which confused me about the meaning of these columns. 

---
 
NCBI_Gene_ID and Annot_Gene_ID and analogously the Gene Symbol vs. Annot. Symbol.

The ORFs came to us from various sources, the largest being from DFCI (which they got from MGC) and they came with prior annotations (the
"Annot." versions I believe). 
We then did our own annotations based on the actual sequence.

In this table, for roughly 16K of these ORFs, the prior annotation exactly matches ours, and for another ~1300 they are non-human gene ORFs such as HcRed and have no prior annotation listed.
But for a few hundred there is a results listed in both columns and there is a discrepancy.
I looked at one example of a discrepancy and one annotation was ELOA3C (ID=107983955) and the other is ELOA3B (ID=728929)
so in that case presumably these are very similar sequences.

---

We took a polyclonal ORF library, which had its own annotation based on (1) the intended gene-specific PCR primers and (2) short read sequencing into a small part of the ORF.
In producing the library that your work is now using, we first isolated the clonal version of the polyclonal library, and then sequenced each clone full-length.
The resulting clonal library was given a rightful annotation based on our full-length sequencing of it.
In most cases the original annotations match our new annotations.
But as you can see, there are cases where they differ - and you should stick with our annotation.

Taking this sample in your file as an example,

| Plate Name       | Row | Col | Name                 | Public ID          | Vector  |
|------------------|-----|-----|----------------------|--------------------|---------|
| OAA01.02.03.04.A | F   | 7   | ORF015027.1_TRC304.1 | ccsbBroad304_05733 | pLX_304 |

columns G-K have the annotation based on our sequencing:

| Transcript     | Symbol | NCBI Gene ID | Taxon ID | Gene Description           |
|----------------|--------|--------------|----------|----------------------------|
| NM_001354366.1 | ELOA3C | 107983955    | 9606     | elongin A3 family member C |

columns L-M have the 'original' annotations inherited from the polyclonal library.

| Annot. Gene Symbol | Annot. Gene ID |
|--------------------|----------------|
| ELOA3B             | 728929         |

---

> we first isolated the clonal version of the polyclonal library, and then sequenced each clone full-length. The resulting clonal library was given a rightful annotation based on our full-length sequencing of it.

I noticed that for the specific example you cited, a clone search on https://portals.broadinstitute.org/gpp/public/clone/search for ccsbBroad304_05733 shows that the "Sequenced %" = 0 (and there are no upper case bases – which indicate empirically verified sequence – in the sequence information at https://portals.broadinstitute.org/gpp/public/clone/details?cloneId=ccsbBroad304_05733).

---

We started with a polyclonal library in pDONR223 (also known as 'Entry' library).
We made a clonal Entry library and tried to sequence this clonal entry library - the majority of the Entry library was full-length sequenced, while a small portion of it were not sequenced - we annotated the status of the sequencing coverage in our web  query results.
When the Entry library was propagated into expression vectors through LR, the tentative sequence of the ORF was passed down from the entry library to the expression library - in 'lowercase'.
Only when there are sequences directly obtained from sequencing the specific expression library, will these bases be in UPPERCASE.
Of pLX304 library, we did not sequence the library fully.
We relied on the fidelity of LR reaction and we did some sampling sequencing to know so. So the sequences you saw from pLX304 library are vastly lowercase, as they were inherited from the Entry library data.

---

In this specific case (a random example) we are honing in on,

- This pLX304 construct: ccsbBroadEn_05733 was derived from this pDONR223 construct ccsbBroadEn_05733
- the sequence for ccsbBroad304_05733 was passed down from ccsbBroadEn_05733, in lowercase
- ccsbBroadEn_05733 was almost fully sequenced
- ccsbBroad304_05733 was not sequenced at all

Is all that correct?

---

You are almost right. except one correction note, and one explanation note below in red:

In this specific case (a random example) we are honing in on,

- This pLX304 construct: ~~ccsbBroadEn_05733~~ ccsbBroad304_05733  was derived from this pDONR223 construct ccsbBroadEn_05733
- the sequence for ccsbBroad304_05733 was passed down from ccsbBroadEn_05733, in lowercase
- ccsbBroadEn_05733 was almost fully sequenced, In this case, the ORF plus 20ish base flanks are fully sequenced, as the uppercase letters indicate.
- ccsbBroad304_05733 was not sequenced at all.

</details>
