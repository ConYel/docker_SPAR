# docker_SPAR
SPAR: small RNA-seq portal for analysis of sequencing experiments
(Forked from wanglab-upenn bitbucket, https://bitbucket.org/wanglab-upenn/spar_pipeline/src/master/)
* publication: https://academic.oup.com/nar/article/46/W1/W36/4992647
* SPAR Pipeline : https://github.com/ConYel/spar_pipeline 
* SPAR Prepare : https://github.com/ConYel/spar_prepare

docker file for the SPAR workflow

## setup docker
Create a new dir 
* `mkdir my_docker_cont`
* `cd my_docker_cont`
* `git clone https://github.com/ConYel/docker_SPAR.git`
* `docker build --tag spar_cont:v1  ./docker_SPAR`
* `mkdir -vp my_data/genome  my_data/samples  my_data/SPAR_res # main directory with data and ref gen files which will be mounted on the container`

### Next steps
####  1. Prepare reference genome
* `cd my_data/genome`
* `wget http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/twoBitToFa`
* `chmod a+x twoBitToFa`
* `wget http://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.2bit`
* `./twoBitToFa hg38.2bit hg38.fa`
####  2. Prepare conservation tracks
* `wget http://hgdownload.cse.ucsc.edu/goldenpath/hg38/phastCons100way/hg38.phastCons100way.bw`
####  3. Prepare STAR index
* `mkdir -p hg38/star`
* `STAR --runMode genomeGenerate --genomeDir hg38/star --genomeFastaFiles hg38.fa --runThreadN 4`

## Run the container and mount the directory 
* `docker run --name spar --rm -ti --mount -v "$PWD/my_data":/home/my_data spar_cont`

The config.docker.hg38.sh can be used to run the workflow please make sure that you have given
the same names of the virtual docker folder ~ "my_data"



Corrections/suggestions are welcome, please make a new branch and then a pull request
