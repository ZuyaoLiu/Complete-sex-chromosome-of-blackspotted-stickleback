# Assembling the Y chromosome of the blackspotted stickleback (<i>Gasterosteus wheatlandi</i>)

## Background
Assembling Y chromosomes is a tricky task. Sex chromosomes often contain large regions which do not recombine between the X and Y (or Z and W). In these regions the gametologs differentiate from one another, resulting in high heterozygosity and eventually hemizygostiy. However homology is often retained. The result is a chromosome with interpsersed regions of homology, heterozygosity and hemizygosity. This causes many problems for assemblers. The heterozygous regions create complex assembly graphs which cannot be resolved easily, and this often results in chimeric contigs and scaffolds, containing portions of both gametolg haplotypes. 

What is needed is a way to phase the assembly of this region. One way often used for this is sequencing triplets or quartets, whereby an XY male is sequenced for assembly e.g. PacBio + HiC, and then WGS (whole genome sequencing) or long read seq is performed for a female, and for one son and one daughter from the cross of those individuals. This way the Y allele always be phased, as long as it can be genotyped in the son. 

However, in many cases, crosses are not available, as with the blackspotted stickleback here. We therefore developed a workflow to use an existing WGS dataset from males and females from a wild population (i.e. not crosses), to construct a phased assembly of the sex chromosome. 

The workflow is laid out below:

![Phased Y assemnbly pipeline](https://github.com/ZuyaoLiu/Evolution-of-magic-sex-chromosomes-of-stickleback/blob/main/Magic%20Y%20pipeline_DLJ.png)
