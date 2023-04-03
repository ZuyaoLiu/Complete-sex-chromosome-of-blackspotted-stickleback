# Assembling the Y chromosome of the blackspotted stickleback (<i>Gasterosteus wheatlandi</i>)

Zuyao Liu & Daniel L. Jeffries (daniel.jeffries@unibe.ch)


## Background
Assembling Y chromosomes is a tricky task. Sex chromosomes often contain large regions which do not recombine between the X and Y (or Z and W). In these regions the gametologs differentiate from one another, resulting in high heterozygosity and eventually hemizygostiy. However homology is often retained. The result is a chromosome with interpsersed regions of homology, heterozygosity and hemizygosity. This causes many problems for assemblers. The heterozygous regions create complex assembly graphs which cannot be resolved easily, and this often results in chimeric contigs and scaffolds, containing portions of both gametolg haplotypes. 

What is needed is a way to phase the assembly of this region. One way often used for this is sequencing triplets or quartets, whereby an XY male is sequenced for assembly e.g. PacBio + HiC, and then WGS (whole genome sequencing) or long read seq is performed for a female, and for one son and one daughter from the cross of those individuals. This way the Y allele always be phased, as long as it can be genotyped in the son. 

However, in many cases, crosses are not available, as with the blackspotted stickleback here. We therefore developed a workflow to use an existing WGS dataset from males and females from a wild population (i.e. not crosses), to construct a phased assembly of the sex chromosome. 

## Assembl-Y workflow

The workflow is laid out below:

![Phased Y assemnbly pipeline](https://github.com/ZuyaoLiu/Evolution-of-magic-sex-chromosomes-of-stickleback/blob/main/Assembl-Y_pipline.png)

The general approach consits of 3 steps:

1. Identify putatively male specific Kmers from the population-level WGS data. 
2. Align these Kmers to the raw PacBio and Hi-C data, and pull out putatively male-specific (i.e. Y-specific) reads. 
3. Use the putatively Y-specific reads to assembly the Y, and use the remaining reads to assemble the autosomes and X.

There is an additional step in there, but before we describe this we need to breifly discuss the issue of differing levels of divergence throughout the sex chromosome. 

## Sex chromosome divergence, and implications for assembl-Y

As mentioned, sex chromosomes consit of interspersed regions with differing levels of homology, from complete homology, to hemizygosity. Our approach of using Kmers to extract Y-specific reads will work well in regions where the Y either has Y-specific sequence, not found on the X, or where the region is still diploid, but contains many Y-specific variants. In both cases these regions will have an abundance of Y-specific kmers in the WGS dataset, and thus we will be able to efficiently identify Y-specific reads for these regions. 

However, there will also likely be regions with very high homology. How often these occur is difficult to predict, and will differ by species, but even if rare, these regions have the potential to break the phased Y assembly. The reason being, there will be very few Y-specific Kmers here, so we will not be able to efficiently identify Y-specific reads, and thus there will be no reads to span this region in our Y-specific read assembly. 

Our solution to this is to use a phasing approach, on the Autosome + X assembly, to identify heterozygous regions in the X assembly. The resulting X-assembly will contain the X haplotype, and then haplotigs, which should represent portions of the Y. We therefore pull out the reads contributing to these haplotigs, and add them to our Y-specific read pool. 

## Validation

We are still in the process of validating each step, and the final assembly. But below are the statistics, and plots that we have generated so far. 

|             | Autos & X  |  Y  | 
| Genome size |            |     |
| N50         |            |     |
| BUSCO       |            |     |









