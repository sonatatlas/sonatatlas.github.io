---
layout: post
categories: react
title: create-react-app
---
though the offiical said that we should judege using redux or not after thinking of if we really need it. most of my projects can't abandon redux. andway, `create-react-app` did well. but anytime I start-up a new project, it takes me a few minutes to change the content of App.js/index.js and I used to delete some useless files. so I init this project to fixed my environment.
First time I tried to create a new wheel, just like create-react-app lol~ Soon I found this cost a lot. I decide to set up my usual files structure as the first-step.

tried to understand the structure of create-react-app

# reaquire modules
+ validate-npm-package-name
+ chalk
+ commander
+ fs-extra
+ path
+ child_process
+ cross-spawn
+ semver
+ dns
+ tmp
+ tar-pack
+ url
+ hyperquest
+ envinfo

# vars 
+ program
+ hiddenProgram

# functions
+ printValidationResults(results)
+ createApp(name, verbose, version, useNpm, template)
+ shouldUseYarn()
+ install(root, useYarn, dependecies, verbose, isOnline)
+ run(root,appName, version, verbose, originalDirectory, template, useYarn)
+ getInstallPackage(version, originalDirectory)
+ getTemporaryDirectory()
+ extractStream(stream, dest)
+ getPackageName(installPackage)
+ checkNpmVersion
+ checkNodeVersion
+ checkAppName(appName)
+ makeCaretRange(dependencies, name)
+ setCaretRangeForRuntimeDeps(packageName)
+ isSafeToCreateProjectIn(root, name)
+ getProxy
+ checkThatNpmCanReadCwd
+ checkIfOnline(useYarn)
