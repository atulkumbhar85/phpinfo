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
