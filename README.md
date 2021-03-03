# minimalplone4mrbob
This is a minimal buildout configuration for installing the latest Plone 4 and bobtemplates.kitconcept.

## Prerequisites

- Python Python 2.7
- Python virtualenv
- Git

## Install
```bash
$ git clone git@github.com:mschmidt42/minimalplone4mrbob.git
$ cd minimalplone4mrbob
$ virtualenv .  # Make sure, it's installing Python 2.7
$ ./bin/pip install -r https://dist.plone.org/release/4-latest/requirements.txt
$ ./bin/buildout
 ```

## Start
```bash
$ ./bin/instance start
 ```
 
 - Or for debugging
```bash
$ ./bin/instance fg
 ```
 
 - Point your webbrowser to http://localhost:6080 (username admin, password
  admin) and install a Plone instance.

## Creating a addon package in src

In the example, the package is called my.package and is located on the filesystem.

```bash
$ ./bin/instance stop
$ mkdir src
$ cd src
$ ../bin/mrbob -O my.addon bobtemplates:plone_addon
 ```
- Choose 'Basic'

## Including the package

In the example, the package is called my.package and is located on the filesystem.

```bash
$ cd ..
$ vi dev.cfg
```
```bash
[buildout]
extends = buildout.cfg

auto-checkout +=
    my.package

test-eggs +=
    my.package [test]

[instance]
eggs +=
    my.package

[sources]
my.package = fs my.package path=src
```

```bash
$ ./bin/buildout -c dev.cfg
```
