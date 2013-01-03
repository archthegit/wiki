## client.properties
This property file is used to configure which client and context to use.  
The default implementation is to use an AWS Client, equaling an optional property like the following:
```
    simianarmy.client.context.class=com.netflix.simianarmy.basic.BasicContext
```
In order to use the AWS client, skip this property and use the default.
In order to use the VSphere Client instead, change this property to
```
    simianarmy.client.context.class=com.netflix.simianarmy.client.vsphere.VSphereContext
```
### AWS Client Properties
These are the properties needed to access Amazon EC2, Amazon Auto Scaling and Amazon SimpleDB. You have to configure this if you use the AWS client.
Even if the VSphere Client is used instead of the AWS client,  the ```simianarmy.client.aws.*``` and ```simianarmy.sdb.domain``` properties still have to be configured since ChaosMonkey uses these credentials to read and write state data to an Amazon SimpleDB.
 
#### simianarmy.client.aws.accountKey
The Access Key Id from [AWS Security Credentials](https://portal.aws.amazon.com/gp/aws/securityCredentials).
```
    simianarmy.client.aws.accountKey = accountKey
```
#### simianarmy.client.aws.secretKey
The Secret Access Key Id from [AWS Security Credentials](https://portal.aws.amazon.com/gp/aws/securityCredentials).
```
    simianarmy.client.aws.secretKey = secretKey
```
#### simianarmy.client.aws.region
This specifies the Amazon region where the Monkeys will run.  It is expected that if you want to run the monkeys in multiple regions then you will a separate installation of SimianArmy in each region.  The default region is "us-east-1".
```
    simianarmy.client.aws.region = us-east-1
```
### VSpehere Client Properties
When using the VSphere Client, the client has to be configured with the following VSphere Client specific properties. As stated above, in addition the aws client properties to access the Amazon SimpleDB also have to be correctly configured.

#### simianarmy.client.vsphere.url
This is the URL to the API of your VSphere instance. The client will use this URL to open connections and issue termination commands.
```
    simianarmy.client.vsphere.url=https://YOUR_VSPHERE_SERVER/sdk
```
#### simianarmy.client.vsphere.username
The username used to authenticate against the API of your VSphere instance.
```
    simianarmy.client.vsphere.username=YOUR_SERVICE_ACCOUNT_USERNAME
```
#### simianarmy.client.vsphere.password
The password used to authenticate against the API of your VSphere instance.
```
    simianarmy.client.vsphere.password=YOUR_SERVICE_ACCOUNT_PASSWORD
```
#### simianarmy.client.vsphere.terminationStrategy.property.name
The VSpehere client uses a TerminationStrategy for terminating VirtualMachines. There currently is only one termination strategy. This ```PropertyBasedTerminationStrategy``` sets a property in the VirtualMachine to a specific value as a trigger and restets the VM. The underlying infrastructure automation is responsible to respond to the trigger by deleting the VM or kickstarting it for reinstallation.
You can configure which property and value will be set prior to resetting the VirtualMachine.

#### simianarmy.client.vsphere.terminationStrategy.property.name
The name of the property to set. The default is "Force Boot".
```
    simianarmy.client.vsphere.terminationStrategy.property.name=Force Boot
```
#### simianarmy.client.vsphere.terminationStrategy.property.value
The value of the property to set. The default is "server".
```
    simianarmy.client.vsphere.terminationStrategy.property.value=server
```