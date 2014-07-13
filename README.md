Impala
======

Real-time Query for Hadoop.  


## Building impala on Fedora 20 (similar directions will apply to Debain based distros)

git clone https://github.com/cloudera/impala

cd Impala

yum install -y boost-devel gcc-c++ thrift

./buildall.sh

## Shortcut to Building the Impala Jar replacement for HCFS


### The right directions might look like this.

cd Impala/fe

source ../bin/impala-config.sh

mvn package -DskipTests=true

...

### Instead, however, a shortcut to build a single class replacement for HDFSUri.java

cd Impala/fe

Edit HDFSUri (remove DistributedFileSystem casts)

remove from the build path all files other than HDFSUri

mvn package -DskipTests=true

### Now in target/ you should see the Impala jar

You can then use classes in this jar and find a way to use a classloaderor other jar hack to run 


### The thrift part of impala is not well documented yet, and seems to be implemented by the "buildall.sh",
### buildall.sh is tricky to get working.  So instead, you can Download a copy of the impala jar to the 
### "impala-frontend-0.1-SNAPSHOT.jar" location below.
### This allows you to get around having to use thrift to compile all the java files from scratch.

mvn instal:install-file -Dfile=../common/impala-frontend-0.1-SNAPSHOT.jar -DgroupId=jay -DartifactId=impala -Dpackaging=jar -Dversion=0.0

## For directions on setting up Impala, see

http://www.cloudera.com/content/support/en/documentation/cloudera-impala/cloudera-impala-documentation-v1-latest.html

