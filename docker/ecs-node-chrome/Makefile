VERSION=3.8.1
REGION=us-west-2
ACCOUNT_ID=111122223333
REGISTRY=$(ACCOUNT_ID).dkr.ecr.$(REGION).amazonaws.com

clean:
	rm -rf common

build:
	mkdir -p common/
	rsync -av --exclude='selenium' --exclude='Makefile' ../common/* common/
	docker build -t ecs-node-chrome --build-arg VERSION=$(VERSION) .
	rm -rf common/

tag: build
	docker tag ecs-node-firefox $(REGISTRY)/ecs-node-chrome:$(VERSION)
	docker tag ecs-node-firefox $(REGISTRY)/ecs-node-chrome:latest

push: tag
	docker push $(REGISTRY)/ecs-node-chrome:$(VERSION)
	docker push $(REGISTRY)/ecs-node-chrome:latest
