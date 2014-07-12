Impala
======

Real-time Query for Hadoop.  


## Building impala on Fedora 20 (similar directions will apply to Debain based distros)

git clone https://github.com/cloudera/impala

cd Impala

yum install -y boost-devel gcc-c++ 

./buildall.sh

## Building the Impala Jars.

cd Impala/fe

source ../bin/impala-config.sh

mvn package -DskipTests=true

## For directions on setting up Impala, see

http://www.cloudera.com/content/support/en/documentation/cloudera-impala/cloudera-impala-documentation-v1-latest.html

