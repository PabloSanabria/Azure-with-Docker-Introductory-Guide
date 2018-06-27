# First Part: Introduction
The objective of this guide is to provide the necessary theoretical and practical information about the operation of the Azure Functions with Docker so that whoever reads it has the possibility of learning the basics and then if you want to be able to deepen in more advanced knowledge.

## What is [Azure](https://azure.microsoft.com/en-us/overview/what-is-azure/)?
Cloud computing is the delivery of computing services—servers, storage, databases, networking, software, analytics, and more—over the Internet (“the cloud”). Companies offering these computing services are called cloud providers and typically charge for cloud computing services based on usage, similar to how you’re billed for water or electricity at home.

Azure is a cloud computing service created by Microsoft for building, testing, deploying, and managing applications and services through a global network of Microsoft-managed data centers. It provides software as a service (SaaS), platform as a service (PaaS) and infrastructure as a service (IaaS) and supports many different programming languages, tools and frameworks, including both Microsoft-specific and third-party software and systems.

You can create your Azure free account o buy it [here](https://azure.microsoft.com/en-us/free).

## What is [Docker](https://www.docker.com/what-docker)?
Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. Docker is also a company that promotes and evolves this technology. Docker works in collaboration with cloud, Linux, and Windows vendors, including Microsoft. The Docker image containers are comprised by: the application itself and its dependencies, and each of these containers use shared operating systems.

**Why it matters:**
Since containers require far fewer resources (they all run on the same OS instance), they start fast and are easy to deploy. Low resource usage allows higher density. You can run more services on the same hardware unit and reduce costs. The main goal of a container image is that it makes the environment (dependencies) the same across different deployments. This means that you can debug it on your machine and then deploy it to another machine with the same environment guaranteed.

![imagedocker](https://user-images.githubusercontent.com/32108894/41814405-63fb28fa-7721-11e8-8495-4c81ec728dbd.png)

#### [Docker deploys containers at all layers of the hybrid cloud](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/docker-defined)

### Main components of Docker

**IMAGE: **
Read-only template used to create containers. To give clarity, we can say that an image is the necessary environment for a certain application to work.

**CONTAINER: **
These are isolated processes initiated from an image.

### Docker Vs Virtual Machine
The big difference is that a virtual machine needs to contain the entire operating system while a Docker container takes advantage of the operating system on which it runs, shares the kernel of the host operating system and even part of its libraries
![imagen-docker-00](https://user-images.githubusercontent.com/32108894/41824616-81b58e26-77e9-11e8-8ac2-ce696cd83e54.png)

To instal Docker on Windows follow steps in that link:  [![dockerstore](https://user-images.githubusercontent.com/32108894/41879833-a8aa4e40-78b1-11e8-83b9-1be3f78b1d3e.PNG) ](https://store.docker.com/editions/community/docker-ce-desktop-windows)

# Second Part: Azure Functions on a Docker Container

Azure functions is used to run a small portion of code in the cloud without worrying about infrastructure and server maintenance
it allows deploy a simple HTTP Trigger on a Docker Container, which will allow us to have full control of the runtime environment and get total abstraction from the OS.

***Why it matters:***
You can write the code you need for the problem at hand (using your language of choice, such as C#, F#, Node.js, Java, or PHP), without worrying about a whole application or the infrastructure to run it.
So, having the convenience of writing JUST the code we need, combined with the ease of deployment of Docker, we can take our app development and supporting skills to a new level.


## Let's do it

First, at this [LINK](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-your-first-function-visual-studio) you could see how to create a first function in Visual Studio, you too can use the Azure portal, Azure CLI, Java and Maven and on Linux using the Azure CLI. 

Let’s start by taking a simple Azure Function function and creating a container for it. But before building the Docker Image, make sure to edit the project’s [function.json](https://github.com/Azure/azure-functions-host/wiki/function.json) and change 'authLevel' to ‘anonymous’. for example:

```xml
{    
    "disabled": false,
    "bindings": [
        {
            "authLevel": "anonymous",
            "name": "req",
            "type": "httpTrigger",
            "direction": "in",
            "methods": [
                "get",
                "post"
            ]
        },
        {
            "name": "$return",
            "type": "http",
            "direction": "out"
        }
    ]
}
```

1. Install Docker on your computer, restart it, and make sure the service is running.

2. Create a Dockerfile in your project folder and add the text below:

```xml
FROM microsoft/azure-functions-runtime:v2.0.0-beta1
ENV AzureWebJobsScriptRoot=/home/site/wwwroot 
COPY . /home/site/wwwroot
```
3. Now, open a command prompt and navigate to your project folder.

4. Use the following commands to build and run your Docker image:

```xml
docker build -t MY_FUNCTION .
```
And, to deploy your function:

```xml
docker run -p 8080:80 MY_FUNCTION
```
5. Now, if you open a browser and go to http://localhost:8080 you should see your function’s result.

6. Done! You are running your Azure function from a Docker container. And just as it worked in your development environment, it will run in the Cloud.

You could also test your function by going to http:localhost:8080/api/MY_FUNCTION?name=MY_NAME and you should see your Azure Function working just like it should.

# Final Conclusion
Running Azure Functions with Docker is very important for developers because it can be done in any part, **also in the cloud**, in an agile and efficient way with a efficient transport and highly portable. Allowing you to focus on developing your code without worrying about whether that code will work on the machine it will be executed on. As we saw you can run an Azure Functions whith Docker in 3 simple steps. Docker can provide cost saving advantages. Containers are a solution to implementation problems as they eliminate friction caused by a lack of dependencies in production environments. By eliminating those problems, it significantly improves development and testing and production operations.
For all this, Docker container can become the standard implementation unit for any server-based application or service.
