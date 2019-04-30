Bootstrap:docker
From:continuumio/anaconda

%labels
    MAINTAINER Marc Hoeppner <m.hoeppner@ikmb.uni-kiel.de>
    DESCRIPTION Singularity image containing a fork of xHLA
    VERSION 1.0

%environment 
    PATH=/opt/conda/envs/hla-1.0/bin:$PATH
    export PATH

%files
    bin/	/opt
    data/	/opt
    environment.yml	/

%post

apt-get -y install procps    

/opt/conda/bin/conda env create -f /environment.yml
/opt/conda/bin/conda clean -a

'install.packages("devtools", repos="http://cran.r-project.org", clean=TRUE);q()' | R --no-save \
	&& echo 'devtools::install_version("data.table", "1.9.6", repos="http://cran.r-project.org", clean=TRUE);q()' | R --no-save \
	&& echo 'devtools::install_version("lpSolve", "5.6.13", repos="http://cran.r-project.org", clean=TRUE);q()' | R --no-save

'source("http://bioconductor.org/biocLite.R"); biocLite("IRanges", ask = F, suppressUpdates = T, suppressAutoUpdate = T)' | R --no-save
