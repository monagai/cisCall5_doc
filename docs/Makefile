GITBOOK=node_modules/.bin/gitbook

.PHONY: all clean serve

all: node_modules/gitbook-cli
	$(GITBOOK) build
	mv _book docs

clean:
	rm -rf _book docs/*

serve: node_modules/gitbook-cli
	cp ./introduction.md _book/README.md
	cp ./SUMMARY.md _book/
	$(GITBOOK) serve _book

node_modules/gitbook-cli:
	npm install gitbook gitbook-cli

