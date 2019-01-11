# Eclipse Che Extension v02
Custom eclipse che extension 5.13
deprecated: https://github.com/eclipse/che-archetypes
current: https://github.com/che-samples

## Referrences
### Super dev mode
https://gist.github.com/phuongtailtranminh/4ec2cd9f899de48458672410e49711ee#file-che-build-L47
Super dev-mode
>  mvn gwt:codeserver -pl :assembly-ide-war -am -Dmaven.main.skip -Dmaven.resources.skip -Dche.dto.skip -Dskip-enforce -Dskip-validate-sources 


## A. **Sample**
> https://github.com/che-samples
### **1. Menu**
### **2. EmbedJS**

0. Create Project
> git clone https://github.com/che-samples/che-plugin-embedjs.git

1. Build

**First time**

> mvn -T 4C -DskipTests -Dskip-validate-sources clean install

> mvn -T 8C -DskipTests -Dskip-validate-sources clean install

**Super dev mode**
> mvn gwt:codeserver -pl :assembly-ide-war -am -Dmaven.main.skip -Dmaven.resources.skip -Dche.dto.skip -Dskip-enforce -Dskip-validate-sources
2. Run

Asume loading javascript from external source:
> cd $(pwd)/plugin-embedjs-ide/src/main/resources/org/eclipse/che/sample/public

> python -m SimpleHTTPServer 8000
> 
> python -m servit.py 8000

*Then set URI for javascript in Presenter class*

We can also remove che-data if needed

> mkdir ~/che-data
> 
> sudo rm -rf ~/che-data/che-data-9001/*

Finally run docker

> docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v $(pwd)/assembly/assembly-main/target/eclipse-che-6.17.0-SNAPSHOT/eclipse-che-6.17.0-SNAPSHOT:/assembly -v ~/che-data/che-data-9001:/data -e CHE_PORT=9001 -e CHE_DOCKER_IP_EXTERNAL=35.198.236.222 eclipse/che:6.16.0 start --skip:scripts

sudo ifconfig lo0 alias $IP (CHE_HOST)
> sudo ifconfig lo0 alias 192.168.65.2

3. Knowledge
---
### **3. Che Json Plugin**
0. Create Project
> git clone https://github.com/che-samples/che-plugin-json.git
1. Build
* ***First time***
> mvn -T 4C -DskipTests -Dskip-validate-sources clean install
* ***Super dev mode***
> mvn gwt:codeserver -pl :assembly-ide-war -am -Dmaven.main.skip -Dmaven.resources.skip -Dche.dto.skip -Dskip-enforce -Dskip-validate-sources
2. Run 

We can also remove che-data if needed

> sudo rm -rf ~/Documents/che-data/che-data-9003/*

Finally run docker

> docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v /media/luyenchu/Data/Impls/Projects/IntegrationPlatforms/EclipseChe/extensions/che-plugin-json/assembly/assembly-main/target/eclipse-che-6.17.0-SNAPSHOT/eclipse-che-6.17.0-SNAPSHOT:/assembly -v /home/luyenchu/Documents/che-data-9003:/data -e CHE_PORT=9003 eclipse/che:6.16.0 start --skip:scripts

***
## Appendix - DEPERECATED method
**********************************plugin-meny-archetype*******************************
0. Create project
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate -DarchetypeRepository=https://maven.codenvycorp.com/content/groups/public/ -DarchetypeGroupId=org.eclipse.che.archetype -DarchetypeArtifactId=plugin-menu-archetype -DarchetypeVersion=5.13.0 -DgroupId=my.plugin -DartifactId=my-sample-plugin -Dversion=0.1-SNAPSHOT -DskipITs -DinteractiveMode=false
1. Build
	mvn clean install
for faster:
	mvn -T 1C -DskipTests -Dskip-validate-sources clean install

2. Run
docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v /media/luyenchu/Data/Impls/Projects/IntegrationPlatforms/EclipseChe/extensions/my-sample-plugin/assembly-che/assembly-main/target/eclipse-che-0.1-SNAPSHOT/eclipse-che-0.1-SNAPSHOT:/assembly -v /home/luyenchu/Documents/che-data-9008:/data -e CHE_PORT=9008 eclipse/che-cli:5.13.0 start

**********************************plugin-embedjs-archetype*******************************
0. Create project
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate -DarchetypeRepository=https://maven.codenvycorp.com/content/groups/public/ -DarchetypeGroupId=org.eclipse.che.archetype -DarchetypeArtifactId=plugin-embedjs-archetype -DarchetypeVersion=5.13.0 -DgroupId=my.plugin -DartifactId=my-sample-embedjs-plugin -Dversion=0.1-SNAPSHOT -DskipITs -DinteractiveMode=false
1. Build
	mvn -DskipTests -Dskip-validate-sources clean install
for faster:
	mvn -T 4C -DskipTests -Dskip-validate-sources clean install
	mvn -T 1C -DskipTests -Dskip-validate-sources clean install

2. Run
docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v /media/luyenchu/Data/Impls/Projects/IntegrationPlatforms/EclipseChe/extensions/my-sample-embedjs-plugin/assembly-che/assembly-main/target/eclipse-che-0.1-SNAPSHOT/eclipse-che-0.1-SNAPSHOT:/assembly -v /home/luyenchu/Documents/che-data-9001:/data -e CHE_PORT=9001 eclipse/che-cli:5.13.0 start
