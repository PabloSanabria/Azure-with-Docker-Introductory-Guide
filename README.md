# First Part: Introduction
El objetivo de esta guia es de proporcionar la informacion teorica y practica necesaria acerca del funcionamiento de las Funciones Azure con Docker para que quien lo lea tenga la posibilidad de aprender lo basico y luego si lo desea poder profundizar en conocimientos mas avanzados.

## What is [Azure](https://azure.microsoft.com/en-us/overview/what-is-azure/)?
Cloud computing is the delivery of computing services—servers, storage, databases, networking, software, analytics, and more—over the Internet (“the cloud”). Companies offering these computing services are called cloud providers and typically charge for cloud computing services based on usage, similar to how you’re billed for water or electricity at home.

Azure is a cloud computing service created by Microsoft for building, testing, deploying, and managing applications and services through a global network of Microsoft-managed data centers. It provides software as a service (SaaS), platform as a service (PaaS) and infrastructure as a service (IaaS) and supports many different programming languages, tools and frameworks, including both Microsoft-specific and third-party software and systems.

You can create your Azure free account o buy it [here](https://azure.microsoft.com/en-us/free).

## What is [Docker](https://www.docker.com/what-docker)?
Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. Docker is also a company that promotes and evolves this technology. Docker works in collaboration with cloud, Linux, and Windows vendors, including Microsoft.
En el caso de los desarrolladores, el uso de Docker hace que puedan centrarse en desarrollar su código sin preocuparse de si dicho código funcionará en la máquina en la que se ejecutará.

![imagedocker](https://user-images.githubusercontent.com/32108894/41814405-63fb28fa-7721-11e8-8495-4c81ec728dbd.png)

#### [Docker deploys containers at all layers of the hybrid cloud](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/docker-defined)

## Main components of Docker

### Image: 
          Read-only template used to create containers. To give clarity, we can say that an image is the necessary environment for a certain application to work.

### Container: 
            These are isolated processes initiated from an image.

## Docker Vs Virtual Machine
The big difference is that a virtual machine needs to contain the entire operating system while a Docker container takes advantage of the operating system on which it runs, shares the kernel of the host operating system and even part of its libraries
![imagen-docker-00](https://user-images.githubusercontent.com/32108894/41824616-81b58e26-77e9-11e8-8ac2-ce696cd83e54.png)


# Pros of a Docker Container
* You can put anything in there
* Stays locked
* Efficient transport ,  highly portable
* No missing dependencies during deployments
* You can run various versions of libraries
* Reduce compatibily concerns
* Self contained - everything you need is in …
* an isolated environment
* it runs everywhere - **also in the cloud**
* it is (relatively) small and lightweight
* therefore very scalable
* and thus cost-efficient.

To instal Docker on Windows follow steps in that link:  [![dockerstore](https://user-images.githubusercontent.com/32108894/41879833-a8aa4e40-78b1-11e8-83b9-1be3f78b1d3e.PNG) ](https://store.docker.com/editions/community/docker-ce-desktop-windows)

# Second Part: Azure Functions on a Docker Container

Azure functions is used to run a small portion of code in the cloud without worrying about infrastructure and server maintenance
it allows deploy a simple HTTP Trigger on a Docker Container, which will allow us to have full control of the runtime environment and get total abstraction from the OS.

### Azure integration benefits
* Familiar Azure admin user experience.
* Deep integration with the underlying Azure infrastructure—get native infrastructure capabilities without additional configuration.
* Secure and easy-to-manage Azure network and instance configuration.
* Auto-provisioned and auto-configured load balancers.
