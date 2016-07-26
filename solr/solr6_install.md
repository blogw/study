#Install Solr6.1.0 on Ubuntu16.04#
---

###prepare###
- [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
- [http://apache.fayea.com/lucene/solr/6.1.0/](http://apache.fayea.com/lucene/solr/6.1.0/)

###jdk8 install###
	# unzip jdk
	[root@dcd88714ce14 ~]# tar zxvf jdk-8u91-linux-x64.tar.gz
	[root@dcd88714ce14 ~]# mkdir /usr/lib/jvm
	[root@dcd88714ce14 ~]# mv jdk1.8.0_91 /usr/lib/jvm

	# edit profile
	[root@dcd88714ce14 ~]# vi /etc/profile
		export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_91
		export JRE_HOME=${JAVA_HOME}/jre
		export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
		export PATH={JAVA_HOME}/bin:$PATH

	# update-alternatives
	[root@dcd88714ce14 ~]# update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_91/bin/java 300
	[root@dcd88714ce14 ~]# update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_91/bin/javac 300
	[root@dcd88714ce14 ~]# update-alternatives --config java

###solr6 install###
	# install solr service
	[root@dcd88714ce14 ~]# tar xzf solr-6.1.0.tgz solr-6.1.0/bin/install_solr_service.sh --strip-components=2
	[root@dcd88714ce14 ~]# ./install_solr_service.sh solr-6.1.0.tgz
		Solr process 157 running on port 8983
		{
		  "solr_home":"/var/solr/data",
		  "version":"6.1.0 4726c5b2d2efa9ba160b608d46a977d0a6b83f94 - jpountz - 2016-06-13 09:46:58",
		  "startTime":"2016-07-04T07:17:33.093Z",
		  "uptime":"0 days, 0 hours, 0 minutes, 15 seconds",
		  "memory":"75.6 MB (%15.4) of 490.7 MB"}
		
		Service solr installed.

	# solr service status
	[root@dcd88714ce14 ~]# service solr status
		Found 1 Solr nodes:
		
		Solr process 157 running on port 8983
		{
		  "solr_home":"/var/solr/data",
		  "version":"6.1.0 4726c5b2d2efa9ba160b608d46a977d0a6b83f94 - jpountz - 2016-06-13 09:46:58",
		  "startTime":"2016-07-04T07:17:33.093Z",
		  "uptime":"0 days, 0 hours, 1 minutes, 25 seconds",
		  "memory":"12.2 MB (%2.5) of 490.7 MB"}

	# create new instance
	[root@0be5ded50f23:~]# su - solr
	[solr@0be5ded50f23:~]# cd /opt/solr/bin
	[solr@0be5ded50f23:/opt/solr/bin$]# ./solr create -c liferay

###test###
	[root@0be5ded50f23:~]# curl http://localhost:8983/solr/liferay/schema/fields
	
		{
		  "responseHeader":{
		    "status":0,
		    "QTime":31},
		  "fields":[{
		      "name":"_root_",
		      "type":"string",
		      "docValues":false,
		      "indexed":true,
		      "stored":false},
		    {
		      "name":"_text_",
		      "type":"text_general",
		      "multiValued":true,
		      "indexed":true,
		      "stored":false},
		    {
		      "name":"_version_",
		      "type":"long",
		      "indexed":true,
		      "stored":false},
		    {
		      "name":"id",
		      "type":"string",
		      "multiValued":false,
		      "indexed":true,
		      "required":true,
		      "stored":true}]}
###reference###
[How to install and configure Solr 6 on Ubuntu 16.04](https://www.howtoforge.com/tutorial/how-to-install-and-configure-solr-on-ubuntu-1604/)

###author###
[blogw](mailto:blogw@163.com) 2016/07/26