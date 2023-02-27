# xc - Simple, Convenient, Markdown defined task runner. 


[![test](https://github.com/joerdav/xc/actions/workflows/test.yaml/badge.svg)](https://github.com/joerdav/xc/actions/workflows/test.yaml) 
[![docs](https://github.com/joerdav/xc/actions/workflows/docs.yml/badge.svg)](https://github.com/joerdav/xc/actions/workflows/docs.yml)
[![Go Reference](https://pkg.go.dev/badge/github.com/joerdav/xc.svg)](https://pkg.go.dev/github.com/joerdav/xc)
[![Mentioned in Awesome Go](https://awesome.re/mentioned-badge.svg)](https://github.com/avelino/awesome-go)
[![Go Report Card](https://goreportcard.com/badge/github.com/joerdav/xc)](https://goreportcard.com/report/github.com/joerdav/xc)
[![Coverage Status](https://coveralls.io/repos/github/joerdav/xc/badge.svg?branch=main)](https://coveralls.io/github/joerdav/xc?branch=main)

![xc](https://user-images.githubusercontent.com/19927761/156772881-10065864-ff4d-4225-ab2b-5adbbe628845.png)

[Docs](https://xcfile.dev/) | [Getting Started](https://xcfile.dev/getting-started/) | [Github](https://github.com/joerdav/xc)

[![asciicast](https://asciinema.org/a/dNZ5DxyxnXmcqsVE9Qs1IyFzL.svg?autoplay=true&speed=2)](https://asciinema.org/a/dNZ5DxyxnXmcqsVE9Qs1IyFzL?autoplay=true&speed=2)


`xc` is a task runner designed to maximise convenience, and minimise complexity.

Each `xc` task is defined in simple, human-readable Markdown. Meaning that for people without the `xc` tool installed there is a clear source of useful commands in the README.md file.

# Installation

Installation instructions are defined at <https://xcfile.dev/getting-started/#installation>.

# Features

![vscode demo](https://user-images.githubusercontent.com/19927761/214538057-963f9a47-ff95-486c-8856-b90bd358be3f.png)

- Markdown defined tasks.
- Editor tools:
	- VSCode (list and run xc tasks)
	- Vim (recommended config for listing and running xc tasks)

# Example

Take the `tag` task in the [README.md](https://github.com/joerdav/xc#tag) of the `xc` repository:

````
## tag

Deploys a new tag for the repo.

Requires: test

```
export VERSION=`git rev-list --count HEAD`
echo Adding git tag with version v0.0.${VERSION}
git tag v0.0.${VERSION}
git push origin v0.0.${VERSION}
```
````

The task could be run simply with `xc tag`, but a side-effect of it being an `xc` task is that the steps for pushing a tag without the use of `xc` are clearly documented too.

```
$ xc tag
+ go test ./...
?       github.com/joerdav/xc/cmd/xc   [no test files]
?       github.com/joerdav/xc/models   [no test files]
ok      github.com/joerdav/xc/parser   (cached)
ok      github.com/joerdav/xc/run      (cached)
+ export VERSION=78
+ echo Adding git tag with version v0.0.78
Adding git tag with version v0.0.78
+ git tag v0.0.78
+ git push origin v0.0.78 Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:joerdav/xc
 * [new tag]         v0.0.78 -> v0.0.78
```

# Tasks

## test

Test the project.

```
go test ./...
```

## lint

Run linters.

```
golangci-lint run
```

## build

Builds the `xc` binary.

```
go build ./cmd/xc
```

## tag
Deploys a new tag for the repo.

Requires: test
```
export VERSION=`git rev-list --count HEAD`
echo Adding git tag with version v0.0.${VERSION}
git tag v0.0.${VERSION}
git push origin v0.0.${VERSION}
```

## update-nix
Updates nix flake.
```
sh ./update-nix.sh
```

## install-hugo

Install hugo via `go install`.

```sh
go install github.com/gohugoio/hugo@latest
```

## run-docs

Run the hugo development server.

Directory: doc

```sh
hugo serve
```
