# Eclipse SWT for Maven Users

SWT is not available in Maven Central making it difficult to use in Maven projects. Existing maven repos are either not maintained and abandoned, don't have all platforms, don't contain sources, don't contain debug jar, or don't automate downloading and extracting the JARs. 

Looking for the 4.5 milestone (M) and release candidate (RC) releases? [See the dev-releases repository](http://github.com/swt-maven/dev-releases)

This repo contains SWT 4.2 to 4.4.2 on all supported platforms
 
 - Stable releases
  - 4.4.2 - 4 Feb 2015
  - 4.4.1 - 25 Sep 2014 
  - 4.4 - 6 Jun 2014
  - 4.3.2 - 21 Feb 2014 
  - 4.3.1 - 11 Sep 2013 
  - 4.3 - 5 Jun 2013 
  - 4.2.2 - 23 Feb 2012 
  - 4.2.1 - 12 Sep 2011 
  - 4.2 - 8 Jun 2012
 - Platforms
  - org.eclipse.swt.win32.win32.x86
  - org.eclipse.swt.win32.win32.x86_64  
  - org.eclipse.swt.cocoa.macosx
  - org.eclipse.swt.cocoa.macosx.x86_64
  - org.eclipse.swt.gtk.linux.x86
  - org.eclipse.swt.gtk.linux.x86_64
  - org.eclipse.swt.gtk.solaris.sparc
  - org.eclipse.swt.gtk.solaris.x86
  - org.eclipse.swt.gtk.aix.ppc
  - org.eclipse.swt.gtk.aix.ppc64
  - org.eclipse.swt.gtk.hpux.ia64
  - org.eclipse.swt.gtk.linux.ppc
  - org.eclipse.swt.gtk.linux.ppc64
  - org.eclipse.swt.gtk.linux.ppc64le
  - org.eclipse.swt.gtk.linux.s390
  - org.eclipse.swt.gtk.linux.s390x
  - org.eclipse.swt.win32.wce_ppc.arm.j2se (4.2 and 4.2.1 only, see Windows CE section at the end)
  - org.eclipse.swt.win32.wce_ppc.arm.j2me (4.2 and 4.2.1 only, see Windows CE section at the end)
 - Each ZIP is extracted as follows
  - swt.jar - Main JAR
  - swt-debug.jar - Add `<classifier>debug</classifier>` 
  - src.zip - Sources classifier, most IDE's can handle downloading this
 
Want JFace support? Please see [Issue #1](https://github.com/maven-eclipse/maven-eclipse.github.io/issues/1)
  
# Why?
Eclipse has an open bug report to to publish SWT to Maven however its been stalled since 2007: https://bugs.eclipse.org/bugs/show_bug.cgi?id=199302

Currently the only available automated downloader is [swt-release-fetcher](http://github.com/hennr/swt-release-fetcher) which only supports the latest release and is very complex. This has been replaced with a much simpler and more flexible bash script that you can even use to setup your own independent repo 

As of creating this project, existing public SWT maven repositories are not usable
 - https://code.google.com/p/swt-repo/ - Abandoned, last release is 4.4
 - https://github.com/urish/swt-repo - Deleted
 - https://github.com/swt-repo/swt-repo - Abandoned, last release 4.2.2 only for linux
 - https://bitbucket.org/confluenity/maven ([from StackOverflow](http://stackoverflow.com/a/19857630)) - Abandoned, original domain doesn't work, bitbucket repo isn't web accessible, last release is 4.3.1

# How to use
If you were using [swt-repo on Google Code](http://code.google.com/p/swt-repo/) this is a drop in replacement

Add this to your pom.xml:

```
<repositories>
	<repository>
		<id>swt-maven-repo</id>
		<url>http://swt-maven.github.io/maven</url>
	</repository>
</repositories>
```

Then add dependencies for each platform you wish to support. The most common are

```
<dependencies>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.win32.win32.x86</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.win32.win32.x86_64</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.gtk.linux.x86</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.gtk.linux.x86_64</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.cocoa.macosx</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.cocoa.macosx.x86_64</artifactId>
		<version>${swt.version}</version>
	</dependency>
</dependencies>
```

## WCE - Windows CE
**Ignore this section unless your targeting Windows CE**

These were released differently from all other platforms

 - Only released for 4.2 and 4.2.1
 - DLL is a standalone artifact: classifier dll, extension dll
 - No debug jar was released