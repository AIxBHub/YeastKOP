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