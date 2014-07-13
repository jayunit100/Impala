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

Edit the files in "HdfsUri.java" and remove other files (or remove from classpath), so that you are able to create a Jar file which only has one class : HdfsUri.java.

Then, put that jar (with a name which is a lexical predecessor, like impala0.jar) into /usr/lib/impala/, /var/lib/impala/lib , etc - possibly using a symlink, to be clean about it).

Now your fixed up HdfsUri will be in Impalas client.  You need to now make sure that impala reads in the right configuration files.  Otherwise, you'll get a "no scheme for filesystem" error if you have a non hdfs uri.



### The thrift part of impala is not well documented yet, and seems to be implemented by the "buildall.sh",

buildall.sh is tricky to get working.  So instead, you can Download a copy of the impala jar to the 
"impala-frontend-0.1-SNAPSHOT.jar" location below. This allows you to get around having to use thrift to compile all the java files from scratch.

mvn instal:install-file -Dfile=../common/impala-frontend-0.1-SNAPSHOT.jar -DgroupId=jay -DartifactId=impala -Dpackaging=jar -Dversion=0.0

Then, cd fe/ 


## For directions on setting up Impala, see

http://www.cloudera.com/content/support/en/documentation/cloudera-impala/cloudera-impala-documentation-v1-latest.html

