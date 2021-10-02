# phpinfo
# metadata Docker File

GITHUB_USERNAME=atulkumbhar85
GITHUB_PROJECT=phpinfo
NODEPORT=80

git clone https://github.com/${GITHUB_USERNAME}/${GITHUB_PROJECT}
cd ${GITHUB_PROJECT}
git pull

docker image build --file Dockerfile-metadata --tag ${GITHUB_USERNAME}/${GITHUB_PROJECT}:metadata ./
docker container run --cpus 0.05 --detach --memory 10M --name ${GITHUB_PROJECT}_meta --publish ${NODEPORT}:8080 --read-only --rm --volume ${PWD}/src:/src:ro ${GITHUB_USERNAME}/${GITHUB_PROJECT}:metadata
'''
'''
# Docker Compose

export ADVERTISE_ADDR=192.168.0.8
export ENV_FILE=common.env
export GITHUB_PROJECT=phpinfo
export GITHUB_RELEASE=single-line
export GITHUB_SRC=src
export GITHUB_USERNAME=atulkumbhar85
export NODEPORT=80
export WORKDIR=src

cd ${HOME}
git clone https://github.com/${GITHUB_USERNAME}/${GITHUB_PROJECT}
cd ${GITHUB_PROJECT}
git pull

source ${ENV_FILE}
docker stack deploy --compose-file docker-compose.yaml ${GITHUB_PROJECT}_${GITHUB_RELEASE}
