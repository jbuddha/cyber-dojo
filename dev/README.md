
# Building your own cyber-dojo server from source

To get all the source:

```
mkdir src
cd src
git clone https://github.com/cyber-dojo/cyber-dojo.git
./cyber-dojo/dev/git-clone-all.sh
cd ..
```

This will create the following directory structure (each directory holds a git repo):

```
src/collector
src/cyber-dojo
src/commander
src/differ
src/docker
src/grafana
src/nginx
src/prometheus
src/ruby
src/runner
src/runner_stateless
src/sinatra
src/storer
src/web_base
src/web
src/zipper
```

To build your server from these repos, ensure docker and docker-compose are installed, then:

```
src/cyber-dojo/dev/build-all.sh
```

To bring up your server:

```
src/commander/cyber-dojo up
```

- - - -

Each repo in the github cyber-dojo organization builds a single docker image.

These are the main service images:
  * [![Build Status](https://travis-ci.org/cyber-dojo/commander.svg?branch=master)](https://travis-ci.org/cyber-dojo/commander) [commander](https://github.com/cyber-dojo/commander) - receives commands from the [cyber-dojo](https://github.com/cyber-dojo/commander/blob/master/cyber-dojo) shell script
  * [![Build Status](https://travis-ci.org/cyber-dojo/nginx.svg?branch=master)](https://travis-ci.org/cyber-dojo/nginx) [nginx](https://github.com/cyber-dojo/nginx) - fancy internet-facing web-server
  * [![Build Status](https://travis-ci.org/cyber-dojo/web.svg?branch=master)](https://travis-ci.org/cyber-dojo/web) [web](https://github.com/cyber-dojo/web) - simple rails web-server
  * [![Build Status](https://travis-ci.org/cyber-dojo/runner.svg?branch=master)](https://travis-ci.org/cyber-dojo/runner) [runner](https://github.com/cyber-dojo/runner) - runs an avatar's code/tests statefully
  * [![Build Status](https://travis-ci.org/cyber-dojo/runner_stateless.svg?branch=master)](https://travis-ci.org/cyber-dojo/runner) [runner_stateless](https://github.com/cyber-dojo/runner_stateless) - runs an avatar's code/tests statelessly
  * [![Build Status](https://travis-ci.org/cyber-dojo/collector.svg?branch=master)](https://travis-ci.org/cyber-dojo/collector) [collector](https://github.com/cyber-dojo/collector) - collects old docker volumes created by stateful runner
  * [![Build Status](https://travis-ci.org/cyber-dojo/storer.svg?branch=master)](https://travis-ci.org/cyber-dojo/storer) [storer](https://github.com/cyber-dojo/storer) - stores an avatar's code/test files
  * [![Build Status](https://travis-ci.org/cyber-dojo/differ.svg?branch=master)](https://travis-ci.org/cyber-dojo/differ) [differ](https://github.com/cyber-dojo/differ) - diffs an avatar's code/test files
  * [![Build Status](https://travis-ci.org/cyber-dojo/zipper.svg?branch=master)](https://travis-ci.org/cyber-dojo/zipper) [zipper](https://github.com/cyber-dojo/zipper) - creates tgz files for download

These are base images:
  * [![Build Status](https://travis-ci.org/cyber-dojo/docker.svg?branch=master)](https://travis-ci.org/cyber-dojo/docker) [docker](https://github.com/cyber-dojo/docker) - base for commander, runner, collector
  * [![Build Status](https://travis-ci.org/cyber-dojo/ruby.svg?branch=master)](https://travis-ci.org/cyber-dojo/ruby) [ruby](https://github.com/cyber-dojo/ruby) - base for sinatra, web_base
  * [![Build Status](https://travis-ci.org/cyber-dojo/sinatra.svg?branch=master)](https://travis-ci.org/cyber-dojo/sinatra) [sinatra](https://github.com/cyber-dojo/sinatra) - base for storer, zipper, differ, docker
  * [![Build Status](https://travis-ci.org/cyber-dojo/web_base.svg?branch=master)](https://travis-ci.org/cyber-dojo/web_base) [web_base](https://github.com/cyber-dojo/web_base) - base for web

The main service repos each contain a `pipe_build_up_test.sh` script which:
- rebuilds the service's docker image
- starts a container from this server image
- shells into the server container
- runs the server tests (with coverage)
- starts a client container
- shells into the client container
- runs the client tests (with coverage)

- - - -

Image dependencies

![Image Dependency Graph](image_dependency_graph.png?raw=true "image dependency graph")

- - - -

Domain model

![Domain model](domain_model.png?raw=true "domain model")

