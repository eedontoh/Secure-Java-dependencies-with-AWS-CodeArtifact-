# Secure-Java-dependencies-with-AWS-CodeArtifact
## Introducing Today's Project!

In this project, I will demonstrate how to set up code artifact to securely store code
dependencies.

### Key tools and concepts

Services used were ec2 , CodeArtifact and IAM Role and Policy. Key concepts 
learnt includes package management lifecycle, environmental variables, CodeArtifact
Domains, IAM resources use cases among among others

### Project reflection

This project took me approximately 1 hr. The most challenging part was compiling the
maven app. It was most rewarding to go through several series of steps to trouble
shoot issues as they come by along the way

## CodeArtifact Repository

CodeArtifact is package repo for storing artifacts and it's dependencies. Engineering
teams use artifact repositories for reliability, consistency and security.

A domain is a folder for centrally managing multiple repos belonging to thesame
organization or project. This ensures consistency, speed and convenience in applying
security rules to the entire repos. My domain is nextwork

A CodeArtifact repository can have an upstream repository, which is like a backup or
secondary library for the primary repo. My repository's upstream repository is Maven
Central which is like the playstore of the java-world for most java libraries

## CodeArtifact Security

### Issue

To access CodeArtifact, i need an authorization token for the ec 2 .However, I run into
an error when retrieving a token because the ec2 instance  doesn't have permission to retrieve
authorization tokens yet.

### Resolution

To resolve the error with the security token, i wrote an IAM policy for authroization
token among others, assigned it to IAM Role and attached it to the ec 2 instance This
resolved the error because ec 2 is now authorized access AWS CodeArtifact.

It's security best practice to use IAM roles because it is provides fine grained or
granular access to only services, users etc which requires those permissions.

![json policy](https://github.com/user-attachments/assets/a901cf72-1e18-4a2c-8db0-bfa99ca327c9)

## The JSON policy attached to my role

The JSON policy (codeartifact:* actions) grants permission to get
authentication token, locate repos and read packages from repos whiles
(sts:GetServiceBearerToken) allows temporarily elevated access specifically for
CodeArtifact ops.


### To test the connection between Maven and CodeArtifact,

### I compiled my web app using settings.xml

The settings.xml file configures Maven via the CodeArtifact information to connect
to CodeArtifact. It tells Maven, whenever you need to download a dependency, look in
this CodeArtifact repository first, and here's how to authenticate yourself.

Compiling means translating project's code into a language that computers can
understand and run. When you compile project, you're making sure everything is
correctly set up and ready to turn into a working app

![settings xml](https://github.com/user-attachments/assets/d53f9242-75f3-4f29-9a9e-d912c03c30f3)


## Verify Connection

After compiling, I checked out the terminal and maven has been built successfully. 

![build sucess](https://github.com/user-attachments/assets/b6e18618-a808-4246-ae7c-76911d908793)

I noticed all the depencies has been packaged in the packages panel of CodeArtifact
![packages](https://github.com/user-attachments/assets/3ce097d6-8688-4af2-896d-482ac3114781)
