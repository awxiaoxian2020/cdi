MyBatis CDI Extension
=====================

[![Java CI](https://github.com/mybatis/cdi/workflows/Java%20CI/badge.svg)](https://github.com/mybatis/cdi/workflows/Java%20CI)
[![Coverage Status](https://coveralls.io/repos/mybatis/cdi/badge.svg?branch=master&service=github)](https://coveralls.io/github/mybatis/cdi?branch=master)
[![Maven central](https://maven-badges.herokuapp.com/maven-central/org.mybatis/mybatis-cdi/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.mybatis/mybatis-cdi)
[![Sonatype Nexus (Snapshots)](https://img.shields.io/nexus/s/https/oss.sonatype.org/org.mybatis/mybatis-cdi.svg)](https://oss.sonatype.org/content/repositories/snapshots/org/mybatis/mybatis-cdi/)
[![License](http://img.shields.io/:license-apache-brightgreen.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

![mybatis-logo](http://mybatis.github.io/images/mybatis-logo.png)

MyBatis-CDI extension takes care of the lifecycle of MyBatis mappers and SqlSessions. MyBatis components are directly injected into your
CDI beans ready to be used, there is no need to create or destroy them. It also provides local and JTA transaction support based on the
@Transactional annotation.

Compatibility
-------------

| CDI API VERSION         | JDK 17 | JDK 11  | JDK 8  |
| ----------------------- | ------ | ------- | ------ |
| cdi-1.0 (not supported) | N      | N       | N      |
| cdi-1.1                 | Y      | Y       | Y      |
| cdi-1.2                 | Y      | Y       | Y      |
| cdi-2.0 (preferred)     | Y      | Y       | Y      |
| cdi-3.0 (not supported) | N      | N       | N      |
| cdi-4.0 (not supported) | N      | N       | N      |

Jakarta EE support is not yet provided by this framework.

Jdk17+ requires jboss-classfilewriter to be at 1.2.5 or it will error, [classfilewriter](https://github.com/jbossas/jboss-classfilewriter/issues/24)

Building
--------

Maven does not allow multiple auto activated profiles (ie activateByDefault and Jdk).  This project supports 3 different CDI support levels currently
and was set to default to cdi-1.2.  Jdk 8 does not allow add opens and this is needed now for jdk 17.  We further are supporting jakarta EE packaging
in addition to java EE packaging.  This results is a tricky situation.  Therefore, we have opted to no longer use activateByDefault which means a
build without providing a profile will fail with missing classes.  Github actions is provisioned to always provide the specific cdi-api profile.
Any localized usage must now do the same as defined below.

The cdi profile can be cdi-1.1, cdi-1.2, or cdi-2.0 and required to run with any of the following.

- mvn clean install -P"cdi-1.1"
- mvn clean install -P"cdi-1.2"
- mvn clean install -P"cdi-2.0"

Testing with Arquillian
-----------------------

In order to test with Arquillian, one class needs to be added to 'JavaArchive' in order for this to load properly.  Add 'SqlSessionManagerRegistry.class'.

See attachment on https://github.com/mybatis/cdi/issues/86 from 2021-12-30 ArquillianMybatisExample.zip [here](https://github.com/mybatis/cdi/files/7795050/ArquillianMybatisExample.zip).  This is to be run under jdk 8 to be error free but will run as-is under jdk 11 with an invocation error which still allows it to run.  Further updates are needed to get this code example current.

Essentials
----------

- [See the docs](http://mybatis.github.io/cdi/)

Contributed Examples
--------------------

- Ready to deploy sample web app (Jee7): [https://github.com/mnesarco/mybatis-cdi-samples](https://github.com/mnesarco/mybatis-cdi-samples/)
