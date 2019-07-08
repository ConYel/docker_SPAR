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
* 
### Next steps
  1. Prepare reference genome
  2. Prepare STAR index
  3. Prepare conservation tracks
(info about optional steps can be found in SPAR_pipeline)
## Run the container and mount the directory 
* `docker run --name spar --rm -ti --mount type=bind,source="$PWD/my_data",target=/home/my_data spar_cont`

The config.docker.hg38.sh can be used to run the workflow but you need to 
change the directories of the genome reference pointing to the mounted dir ~ "my_data"



Corrections/suggestions are welcome, please make a new branch and then a pull request
