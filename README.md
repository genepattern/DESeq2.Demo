# DESeq2.Demo

Demo wrapper module for the DESeq2 R package


#
# Based on R session history, running DESeq2 as gpbroad on UGER interactive session
#     @see: http://dwheelerau.com/2014/02/17/how-to-use-deseq2-to-analyse-rnaseq-data/
#
# ssh gpbroad@gpbroad-rhel6
# use UGER
# qrsh -q interactive
# use .r-3.0.2-bioconductor-2.13
# R
#

#
#
#
library('DESeq2')
directory <- '/xchip/gpbroad/shared_data/DESeq2'
sampleFiles<-grep('treated',list.files(directory),value=TRUE)
sampleCondition<-c('treated','treated','treated','untreated','untreated','untreated')
sampleTable<-data.frame(sampleName=sampleFiles, fileName=sampleFiles, condition=sampleCondition)
ddsHTSeq<-DESeqDataSetFromHTSeqCount(sampleTable=sampleTable, directory=directory, design=~condition)
colData(ddsHTSeq)$condition<-factor(colData(ddsHTSeq)$condition, levels=c('untreated','treated'))
dds<-DESeq(ddsHTSeq)
res<-results(dds)
res<-res[order(res$padj),]
head(res)

#plotMA(dds,ylim=c(-2,2),main='DESeq2')
#dev.copy(png,'deseq2_MAplot.png')
#library(Cairo)
#help(Cairo)

library(Cairo)
CairoPNG('deseq2_MAplot.png')
plotMA(dds,ylim=c(-2,2),main='DESeq2')
dev.off()

