# Quick Start Guide

This section helps you to quickly set up and run Ballerina so that you can use it for various solutions. Here we 

## Install Ballerina

1. [Download](https://ballerina.io/downloads) Ballerina for your Operating System. 
1. Follow the instructions given in the [Ballerina Getting Started page](#https://ballerina.io/learn/getting-started/) to set it up. 

> **Note**: Throughout this documentation, `<ballerina_home>` refers to the directory in which you just installed Ballerina.

## Set up the Editor

Let's try this on VS Code.

> **Tip:** You can use your [favorite editor to work on Ballerina code](#https://ballerina.io/learn/tools-ides/), however, we recommend you use VS Code as we have made some improvements to it for use in integration scenarios.

1. Open VS Code.
   > **Tip**: Download and install [VS Code](#https://code.visualstudio.com/Download) if you do not have it already.

2. Find the extension for Ballerina in the VS Code marketplace. For instructions on installing and using it, see [The Visual Studio Code Extension](#https://ballerina.io/learn/tools-ides/vscode-plugin/).

The following page appears.

![alt text](../../assets/img/vs-code-landing.png)

You can select one of the available templates or run it using the CLI as indicated in the following section.

## Create a Project, Add a Template, and Invoke the Service

Create a new project by navigating to a directory of your choice and running the following command. 

```bash
$ ballerina new MyProject
```

You see a response confirming that your project is created. 

Navigate into the project directory you created and run the following command. This command enables you to create a module using a predefined template. In this case, we use the `content_based_routing` template.

```bash
$ ballerina add -t wso2/xml_to_json_transformation MyModule
```

This automatically creates a content-based routing service for you inside an `src` directory. A Ballerina service represents a collection of network accessible entry points in Ballerina. A resource within a service represents one such entry point. The generated sample service exposes a network entry point on port 9090.

Navigate to the `src` directory and run the service using the `ballerina run` command.

```bash
$ ballerina build MyModule
```

You get the following output.

```bash
Compiling source
	qsg/MyModule:0.1.0

Creating balos
	target/balo/MyModule-2019r3-any-0.1.0.balo

Running tests
    qsg/MyModule:0.1.0
	No tests found

Generating executables
	target/bin/MyModule-executable.jar
```

Run the following Java command to run the executable .jar file that is created once you build your module.

```
java -jar target/bin/MyModule-executable.jar  -c src/MyModule/ballerina.conf
```

Your service is now up and running. You can invoke the service using an HTTP client. In this case, we use cURL.

```bash
$ curl http://localhost:9090/calculatorService/calculate -H "Content-Type: application/json" --data '{"operation": "add", "valueOne": 20, "valueTwo": 10}' -v
```

> **Tip**: If you do not have cURL installed, you can download it from [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

You get the following response.

```
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 9092 (#0)
> POST /calculatorService/calculate HTTP/1.1
> Host: localhost:9092
> User-Agent: curl/7.54.0
> Accept: */*
> Content-Type: application/json
> Content-Length: 52
> 
* upload completely sent off: 52 out of 52 bytes
< HTTP/1.1 500 Internal Server Error
* no chunk, no close, no size. Assume close to signal end
< 
* Closing connection 0
```

You just started Ballerina, created a project, started a service, invoked the service you created, and received a response.
