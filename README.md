# vro-helloworld-plugin
A hello world project for vRO plugin

Has a greeter service and an inventory of employees.

# To create the plugin
https://code.vmware.com/forums/3055/vrealize-orchestrator#573085

If the following doesnt work and throws the error:  

Failed to execute goal org.apache.maven.plugins:maven-archetype-plugin:3.0.1:generate (default-cli) on project standalone-pom: archetypeCatalog 'https://HOST:8281/vco-repo/archetype-catalog.xml' is not supported anymore. Please read the plugin documentation for details

Change
mvn archetype:generate <parameters> 
To
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate <parameters>

# To build run the following command
mvn clean install -Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true -Drepo.host=<VRO_HOST_IP> -Dbuild.number=1

If you run into maven error:

Unresolveable build extension: Plugin com.vmware.o11n.mojo.pkg:maven-o11n-package-plugin:7.3.0 or one of its dependencies could not be resolved: Could not find artifact com.vmware.o11n.mojo.pkg:maven-o11n-package-plugin:jar:7.3.0

Add the repository id to your settings.xml file. This will ensure that libraries are fetched from vro repo instead of public maven repository.
respsitory id in pom.xml is added-by-archetype. Hence the change:
<mirrorOf>!added-by-archetype,

#To import workflows into project ensure they are mapped to package: com.demo.helloworld then run
mvn o11n-package:import-package -DserverUrl=vsphere.local\\administrator:<password>@<VRO_HOST_IP>:8281 -Dmaven.wagon.http.ssl.insecure=false -Dmaven.wagon.http.ssl.allowall=true
