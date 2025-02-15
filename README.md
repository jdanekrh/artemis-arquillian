# Artemis Arquillian

Artemis Arquillian is an implementation of A JBoss Arquillian Container that allows you to write tests without having to 
programmatically start a broker. It decouples the creation and running of the broker from the test itself so you can write 
and develop tests to run that can run in different environments, single machine, multiple bare metal or Cloiud environments. 

There are 2 deployable containers Local and Remote which are both configured in the Arquillian.xml file.

## Artemis Local Container

The local container will start an Artemis Broker on the host machine where the tests are running. To configure a local 
container you need to make sure its on the classpath, the maven coords are:

```xml
    <groupId>org.apache.activemq.artemis</groupId>
    <artifactId>artemis-local-container</artifactId>
```

The container protocol is configured in the arquillian.xml file via the following:

```xml
    <defaultProtocol type="artemis local"/>
```

There are 2 sets of tests that can be run to test this, the test Category standalone can be run via:

    $ mvn clean package -Pstandalone-local 

which is configured via the arquillian.xml file.

The test Category Replicated6Node which starts 3 pairs of replicated brokers can be run via:

    $ mvn clean package -Preplicated-local 


which is configured via the arquillian6nodereplicated.xml file.

## Artemis Remote Container

The Artemis Remote container will connect and control a broker on a remote machine, for this to work you will need to 
deploy the artemis bootstrapper on the same machine as the broker and start it with the correct configuration. you do this via:

    $ java -DARTEMIS_HOME=/home/ataylor/devtools/artemis-profiles/live -jar artemis-bootstrapper/target/artemis-bootstrapper-swarm.jar
    
The ARTEMIS_HOME property should point to an instance of the broker on the target machine.

You can then run the following    

## Test Suite