puppet-jdk_oracle
=================

Puppet module to install a JDK from the RPM binary distribution from oracle using wget.
Based on the https://github.com/tylerwalts/puppet-jdk_oracle this module removed support for JDK6 and the tgz installer.

Source: http://www.oracle.com/technetwork/java/javase/downloads/index.html

_Note:  By using this module you will automatically accept the Oracle agreement to download Java._

This module will work on Redhat family of OSs, and will use wget with a cookie to automatically grab the RPM installer from Oracle.

This approach was inspired by: http://stackoverflow.com/questions/10268583/how-to-automate-download-and-instalation-of-java-jdk-on-linux


Currently Supported:
* RedHat Family (RedHat, Fedora, CentOS)
* Java 7 and Java 8
* 64 and 32 bit architectures.

Installation:
=============

A) Traditional:
* Copy this project into your puppet modules path and rename to "jdk_oracle"

B) From Puppet Forge
* Install from Puppet Forge:
```
$ puppet module install schrepfler-jdk_oracle
```

C) Puppet Librarian:
* Put this in your Puppetfile:
```
    mod "jdk_oracle",
        :git => "git://github.com/schrepfler/puppet-jdk_oracle.git"
```


Usage:
======

A)  Traditional:
```
    include jdk_oracle
```
or
```
    class { 'jdk_oracle': }
```


B) Hiera:
config.json:
```
    {
        classes":[
          "jdk_oracle"
        ]
    }
```
OR
config.yaml:
```
---
  classes: 
    - "jdk_oracle"
  jdk_oracle::version: "7"
```

site.pp:
```
    hiera_include("classes", [])
```


Parameters:
===========

* version
    * Java Version to install
* install_dir
    * Java Installation Directory
* tmp_dir
    * Temp directory to download the installer, default `/tmp/`
* version7update
    * Latest Java 7 Update version
* version7build
    * Latest Java 7 Build version
* version8update
    * Latest Java 8 Update version
* version8build
    * Latest Java 8 Build version
* arch 
    * parameter to provide support for other architectures, default `x64`
* use_cache
    * Optionally host the installer file locally instead of fetching it each time, for faster dev & test


TODO:
=====

* Automate installation of security policies
* Refactor tests to support some use cases of the tgz module
* 
~~Add support for 32-bit JDK~~
* Add build status icons
* Make it possible to uninstall the jdk package
