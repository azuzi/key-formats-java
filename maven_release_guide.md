# Maven Release Guide

Add the following user credential and repository details to "~/.m2/settings.xml" Replace the [OWNER with github youser name token with Github acces token](https://help.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-apache-maven-for-use-with-github-packages). 
~~~
  <profiles>
    <profile>
      <id>github</id>
      <repositories>
	    <repository>
            <id>github</id>
            <name>GitHub OWNER key-formats-java</name>
            <url>https://maven.pkg.github.com/azuzi/key-formats-java</url>
        </repository>
      </repositories>
    </profile>
  </profiles>
  <servers>
    <server>
      <id>github</id>
      <username> OWNER</username>
      <password>TOKEN</password>
    </server>
  </servers>
~~~

Add the distribution management and SCM (Software Configuration Management) to parent POM file.
~~~~
<scm>
    <url>https://github.com/azuzi/key-formats-java</url>
    <connection>scm:git:git://github.com/azuzi/key-formats-java.git</connection>
    <developerConnection>scm:git:git@github.com:azuzi/key-formats-java.git</developerConnection>
</scm>

<distributionManagement>
    <repository>
      <id>github</id>
      <name>GitHub OWNER key-formats-java</name>
      <url>https://maven.pkg.github.com/azuzi/key-formats-java</url>
    </repository>
</distributionManagement>
~~~~

For each release of new version create a new branch similer ti 0.1.x and update the branch
~~~
git checkout 0.1.x
git push --set-upstream origin 0.1.x
~~~

Make changes related to new version and update the github

Then prepare for release
~~~
mvn release:clean
mvn release:prepare  -Dresume=false
~~~

Finally perform the release.
~~~
mvn release:perform
~~~