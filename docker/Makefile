TAG = latest
ORG ?= ghcr.io/netdrones
IMAGE ?= voxblox
DOCKERFILE ?= Dockerfile

DOCKERNAME = "${ORG}/${IMAGE}:${TAG}"

.PHONY: build
build:
	docker build -t "${DOCKERNAME}" -f "${DOCKERFILE}" ..

.PHONY: run
run:
	sudo sh +x run.sh

.PHONY: download-data
download-data:
	wget http://robotics.ethz.ch/~asl-datasets/iros_2017_voxblox/data.bag

.PHONY: run-test
run-test:
	sudo ./run.sh -v data.bag:/tmp/data.bag
