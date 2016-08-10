# DESeq2.Demo

Demo wrapper module for the DESeq2 R package, developed as a 
proof-of-concept on the Broad compute cluster (rhel6 environment),
with hard-coded datasets, based on Dave Wheeler's Feb 2014 blog post: 
    http://dwheelerau.com/2014/02/17/how-to-use-deseq2-to-analyse-rnaseq-data/

#
# Example interactive session on Broad cluster ...
#

ssh gpbroad@gpboad
use UGER
stty -ixon
ish

# initialize R/3.2.5 environment
# special-case for libxml2, the Broad dotkit was built with a different version of zlib,
# before switching I need to figure out how to easily rebuild all of the R packages from source
# use .libxml2-2.9.4
LIBXML2_HOME='/xchip/gpbroad/packages/libxml2/2.9.4'
export PATH="${PATH}:${LIBXML2_HOME}/bin"
 
use .curl-7.47.1
use .pixman-0.32.6
use .cairo-1.14.2
use .r-3.2.5-vanilla

export R_LIBS=''
export R_LIBS_USER=' '
# use common site-library, for all GP R/3.2 modules
export R_LIBS_SITE=/xchip/gpbroad/servers/gpbroad/patches/uger-rhel6/Library/R/3.2
# alternatively, use a dedicated site-library for DESeq2
#export R_LIBS_SITE=/xchip/gpbroad/servers/gpbroad/patches/uger-rhel6/Library/R/3.2.5-deseq2

