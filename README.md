# custom-jwt-validation-policy

Step 1: Setting Up Base Project For Custom Policy: 
Setting up a project with the Archetype : 
A) We need a project with the required basic custom files.

B) The easiest way to gather all your required files is by using the maven archetype.

Please note Maven archetype is currently unavailable in a Public Maven Central Repository, so we need to configure our settings.xml (Developers Machine) to find the archetype in one of MuleSoft’s repositories.

C) Add the Profile Given below side to Settings.xml

`<!-- Profile for Custom Policy Archetype -->
<profiles>
	<profile>
		<id>archetype-repository</id>
		<repositories>
			<repository>
				<id>archetype</id>
				<name>Mule Repository</name>
				<url>https://repository-master.mulesoft.org/nexus/content/repositories/public</url>
				<releases>
					<enabled>true</enabled>
					<checksumPolicy>fail</checksumPolicy>
				</releases>
				<snapshots>
					<enabled>true</enabled>
					<checksumPolicy>warn</checksumPolicy>
				</snapshots>
			</repository>
		</repositories>
	</profile>
</profiles>`

D) Additional Server and Mule Repo Configurations for Build and Deploy phase :   
 1) You need to add your Anypoint platform credentials as well to your settings.xml. Make sure you replace ${username} and ${password} with actual credentials 
   ` <!– Step D1 Server Profile -->
    <servers>
      <server>
        <id>exchange-server</id>
        <username>${username}</username>
        <password>${password}</password>
      </server>
    </servers>`

 2) One more Private Mule Repository Profile you need to add to your settings.xml.
   `<!- Step D2 Mule Private Repo Profile -->
    <profile>
      <id>Mule</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <repositories>
        <repository>
          <id>MuleRepository</id>
          <name>MuleRepository</name>
          <url>https://repository.mulesoft.org/nexus-ee/content/repositories/releases-ee/</url>
          <layout>default</layout>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
          </snapshots>
        </repository>
      </repositories>
    </profile> `
