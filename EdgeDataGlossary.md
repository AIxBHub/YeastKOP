# YeastKOP
Artifacts and tracking of yeast histone data

# Node Data Glossary

## Genes

### Labels
- ID: SGD:S000006286
- Categories: biolink:Gene
- Name: xxxxx
### Properties
- Namesake: xxxxx
- Protein: xxxxx
- Description: xxxxx
- Organism: S. cerevisiae
- FeatureType: ORF
- Locus: {chr:IV, base_pairs:10101-11011, strand:-1}
- ReferenceLink: xxxxx

## GO Terms

### Labels
- ID: GO:0000127
- Categories: cellular_component, molecular_function, biological_process (need to update to Biolink model)
- Name: xxxxx
### Properties
(None)

## Pathways

### Labels
- ID: PTWY:YEAST-FAO-PWY (No standard ontology, just based on SGD pathway identifiers)
- Categories: biolink:Pathway
- Name: xxxxx
### Properties
- Taxon: NCBI_Taxon:559292
- Organism: S. cerevisiae
- ReferenceLink: xxxxx

## Phenotypes

### Labels
- ID: APO:0000209 (Need to check if handled by node normalizer)
- Categories: biolink:PhenotypicFeature
- Name: actin cytoskeleton morphology
### Properties
- Taxon: NCBI_Taxon:559292
- Organism: S. cerevisiae
- ReferenceLink: xxxxx

## Complexes

### Labels
- ID: EBI:EBI-13924173 (Could switch to SGD identifier, like SGD:S000005329, if that would be easier than adding EBI support)
- Categories: biolink:MacromolecularComplexMixin (Need to check if there is a better option for biolink class)
- Name: xxxxx
### Properties
- Function: xxxxx
- SystematicName:  CDC13:STN1:TEN1
- Properties: xxxxx
- SGDAccessionID': SGD:S000005329 (perhaps switch ID to this)
- Taxon: NCBI_Taxon:559292
- Organism': S. cerevisiae
- ReferenceLink: xxxxx

## Yeast Stress Event

### Labels
- ID: (Could be a chemical substance identifier like PUBCHEM:5353800 for Diamide, or some other identifier for things like heat shock or glucose starvation)
- Categories: biolink:ChemicalEntity, biolink:ExposureEvent, biolink:EnvironmentalExposure (Will need to check these and adjust for migration to Biolink 3.0)
- Name: (Name corresponding to whichever identifier is used)
### Properties
- Concentration: (expressed in Molarity)
- Temperature: (Celsius)
- Growth Medium: YPD, YPG, etc.

## Nucleosomes

### Labels
- ID: NUC:00001 (Since nucleosome peak calling may vary by experimental dataset, could included GEO ID in NUC ID, such as NUC:GSE61888-00001)
- Categories: biolink:GenomicEntity (will need to check on this)
- Name: NUC:00001
### Properties
- Locus: {chr: IV, center: 10101}
- GenePosition: -1
- ReferenceLink: GSE61888 High-Resolution Chromatin Dynamics during a Yeast Stress Response

## Histone PTMs/Variants

### Labels
- ID: GO:0043977  (Already exists GO Terms for the histone PTMs as a process, however may need other ID for histone variants like HTZ1)
- Categories: biolink:BiologicalProcess (will need to check on this)
- Name: histone H2A-K5 acetylation
### Properties
- AssociatedNucleosome: NUC:00001 (or NUC:GSE61888-00001, could use this property to differentiate histone PTMs/Variants, but may need to use unique IDs to do so instead of GO terms)

# Edge Data Glossary

## Gene2GOTerm

### Labels
- Subject ID: SGD:S000006286 (Gene ID)
- Object ID: GO:0000127 (GO Term ID)
- Predicate: involved in, is_active_in, contributes_to, part_of, enables, biolink:actively_involved_in (Need to normalize all these predicates to biolink in the loadYeastSGDInfo.py parser)
### Properties
- EvidenceCode: IGI
- EvidenceCodeText: SGD:S000000384
- AnnotationType: manually curated
- EvidencePMIDs: 21873635

## Gene2Pathway

### Labels
- Subject ID: SGD:S000006286 (Gene ID)
- Object ID: PTWY:YEAST-FAO-PWY (SGD Pathway Identifier)
- Predicate: biolink:participates_in (Check if better predicate exists)
### Properties
(None)

## Gene2Phenotype

### Labels
- Subject ID: SGD:S000006286 (Gene ID)
- Object ID: APO:0000209 (APO Phenotype Identifier)
- Predicate: biolink:genetic_association (Check if better predicate exists)
### Properties
- EffectOnPhenotype: increased
- PhenotypeDetails: actin cables disappear and cortical actin patches become delocalized
- ExperimentType: classical genetics
- MutantType: conditional
- GeneAllele: act1-S14A (Need to see if we can find unique identifiers for these alleles)
- AlleleDescription: ts allele
- YeastStrainBackground: S288c (Need to find unique identifiers for yeast strains)
- ChemicalExposure: 1.8 M glucitol
- ExperimentalCondition: Temperature: elevated temperature (37°C) 
- EvidencePMIDs: 7744777

## Gene2Complex

### Labels
- Subject ID: SGD:S000006286 (Gene ID)
- Object ID: EBI:EBI-13924173 (Need to check if better Identifier exists, like SGD ID)
- Predicate: biolink:in_complex_with (Check if better predicate exists)
### Properties
- GeneBiologicalRole: enzyme
- GeneStoichiometry: 2.0
- InteractorType: protein

## YeastStressor2Nucleosome

### Labels
- Subject ID: (Some Stressor identifier)
- Object ID: NUC:00001 (Or something like NUC:GSE61888-00001 that includes experimental data source)
- Predicate: biolink:affects_molecular_modification_of (Check if better predicate exists)
### Properties
- Occupancy: 3.02
- EpigeneticModifications: {
    H2AK5ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H2AS129ph: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K14ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K18ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K23ac [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K27ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K36me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K36me2: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K36me3: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4me2: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4me3: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K56ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K79me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K79me3: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K9ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3S10ph: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K12ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K16ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K20me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K5ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K8ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4R3me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4R3me2s: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    HTZ1: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)]
} (Could add other histone modifications depending on data availability and adjust for time points measured. Putting Occupancy and EpigeneticModifications as edge properties is one option since these properties are sensitive to the identity of the Yeast Stressor condition.)

## YeastStressor2HistonePTM/Variant

### Labels
- Subject ID: (Some Stressor identifier)
- Object ID: GO:0043977  (Already exists GO Terms for the histone PTMs as a process, however may need other ID for histone variants like HTZ1)
- Predicate: biolink:increases_abundance_of, biolink:decreases_abundance_of (These will be deprecated in Biolink 3.0, check if better predicate exists)
### Properties
- ModificationChange: {
    H2AK5ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H2AS129ph: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K14ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K18ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K23ac [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K27ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K36me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K36me2: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K36me3: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4me2: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K4me3: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K56ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K79me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K79me3: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3K9ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H3S10ph: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K12ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K16ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K20me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K5ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4K8ac: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4R3me: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    H4R3me2s: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)],
    HTZ1: [log2FC(t=0),log2FC(t=4),log2FC(t=8),log2FC(t=15),log2FC(t=30), log2FC(t=60)]
} (Could add other histone modifications depending on data availability and adjust for time points measured. Putting Occupancy and EpigeneticModifications as edge properties is one option since these properties are sensitive to the identity of the Yeast Stressor condition.)

## Nucleosome2Gene

### Labels
- Subject ID: NUC:00001 (Or something like NUC:GSE61888-00001 that includes experimental data source)
- Object ID: SGD:S000006286 (Need to check if better Identifier exists, like SGD ID)
- Predicate: biolink:located_in (Check if better predicate exists)
### Properties
- GenePosition: -1
- GeneFeature: (Not sure how to implement this right now, but could specify if nucleosome is located in gene promoter, TSS, intron, exon, etc.)

## HistonePTM/Variant2Nucleosome

### Labels
- Subject ID: GO:0043977  (Already exists GO Terms for the histone PTMs as a process, however may need other ID for histone variants like HTZ1)
- Object ID: NUC:00001 (Or something like NUC:GSE61888-00001 that includes experimental data source)
- Predicate: biolink:located_in (Check if better predicate exists)
### Properties
(None)