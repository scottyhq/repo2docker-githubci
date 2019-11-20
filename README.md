# repo2docker-githubci
a template for building jupyterhub-compatible docker images with repo2docker and github actions

![Action Status](https://github.com/scottyhq/repo2docker-githubci/workflows/Repo2Docker/badge.svg)

### how to use

1) click the "Use this template" button to create a repo copy

1) create dockerhub account that matches your github username
(could make this configurable)
For example: https://hub.docker.com/u/scottyhq

1) add DOCKER_USERNAME and DOCKER_PASSWORD to repo encrypyted secrets
https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets

1) build with GitHub Action
* commits to master branch trigger re-building image tagged by github short sha and 'latest'
```
git commit -a -m "modified binder/environment to my liking"
git push
```
* pushing a tag results in a docker image with the same tag:
```
git tag -am "test v2.3.2" v2.3.2
git push --tags
```

### grab your image to run locally
```
export IMAGE=scottyhq/repo2docker-github
export TAG=latest
docker pull docker.pkg.github.com/$IMAGE:$TAG
docker run -it --name repo2docker -p 8888:8888 $IMAGE:$TAG jupyter lab --ip 0.0.0.0
docker stop repo2docker
docker rm repo2docker
```

### or run on a binderhub
Just point to the image in a seperate repo containing notebooks you want to run:
https://github.com/scottyhq/githubci-binder-example

