NS = jmlw
VERSION ?= armv7-1.25.2
REPO = ghost-docker-arm

.PHONY: build push shell run start stop rm release

build:
	docker build -t $(NS)/$(REPO):$(VERSION) .
push:
	docker push $(NS)/$(REPO):$(VERSION)

default: build

