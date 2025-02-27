> [Azure Fundamentals Part 3: Describe Core Solutions and Management Tools in Azure](https://docs.microsoft.com/en-us/learn/paths/az-900-describe-core-solutions-management-tools-azure)  
> Microsoft Learn

[TOC]

# Choose the Best Azure IoT Service for your Application

## Identify the Product Options

IoT enables devices to gather and then relay information for data analysis. 
Commons sensors

* Environmentsl sensors that capture temperature and humidity levels
* Barcode, QR code, OCR (optical character recognition) scanners
* Geo-location and proximity sensors
* Ligh, color and ifrared sensors
* Sounds and ultrasonic sensors
* Motion and touch sensors
* Accelerometer and tilt sensors
* Smoke, gas and alcohol sensors
* Error sensors to detect when there's a problem with the device
* Mechanical sensors that detect anomalies or deformations
* Flow, level and pressure sensors for measuring gasses and liquids

Devices can send their readings to a specific endpoint on Azure IoT via a message. CAn update devices with new firmware by sending software updates from Azure IoT to each device.

Suppose we manufacture a smart vending machine, we'd like to collect information like:
* Each machine operating without errors?
* Have they been compromised?
* Is the refrigreration system working as intended?
* Item stock levels

Sending the above information as a message to Azure IoT can be received, stored, organized and displayed but can also be combined with Azure AI services to help predict:
* When maintenance may be required
* When inventories will need to be replenished

### Azure IoT Hub

Acts as a central message hub for bi-directional communication between IoT application and the devices it manages. Device agnostic so the sky is the limit.

Supports communication from the device to the cloud and from the cloud to the device and supporting multiple messaging patterns like device-to-cloud telemetry, file upload from devices and request-reply methods. IoT hub can route the messages received to other Azure services.

### Azure IoT Central

Builds on top of IoT Hub by adding a dashboard to connect, monitor and manage IoT devices. Can watch overall performance across all devices in aggregrate and can set up alerts that send notifications when devices need maintenance and also being able to push firmware updates.

Providing common scenario templates across different industries to quickly be up and running. Can manage devices remotely via the UI but the key part of IoT Central is the use of device templates. Connect a device without any service-side coding to construct the dashboards, alerts and so forth though developers still need to create the code to run on the devices and must match the template specification.

### Azure Sphere

Creates end-to-end, highly secure IoT solution for customers that encompasses everything from hardware and OS on the device to the secure method of sending messages to the hub.

<div align="center" style="min-width: 700px; background: #FFF; color: #000;">
	<img src="./assets/MT3620.png" />
	<p>
		<small>Seeed Azure Sphere MT3620 Development Kit MCU</small>
	</p>
</div>

* Comes with a micro-controller unit (MCU) which processes the OS and signals from the attached sensors. 
* Custom Linux OS that handles communication with the security service and run the vendor's software
* Azure Sphere Security Service (AS3) which is responsible for ensuring the device has not been compromised. Authenticates itself with Azure via certificate-based authentication.

## Analyse the Decision Criteria

Understanding criteria needed can help in making the decision for which IoT service to use.

### Is it critical to ensure that the device is not compromised?

Not all cases, though it would be nice not to be compromised nefariously, but as an example a washing machine wouldn't need to be as security oriented as an ATM.

If security is critical, the best option would be Azure Sphere, which provides a comprehensive end-to-end solution for IoT devices. Ensuring a secure channel of communication between the device and Azure by having control of the hardware, OS and authentication process.

### Do I need a dashboard for reporting and management?

If the end goal is to receive telemetry data and push occasional updates then Azure IoT Hub will be great by itself and can offset management tools and reports to developers via the IoT Hub RESTful API.

If it's a pre-built customizable UI that lets you control devices remotely, then Azure IoT Central is the service needed. Which integrates with IoT Hub to create a reporting dashboard and management.

# Choose the Best AI Service for your Needs

## Identify the Product Options

AI is a broad classification of computing that allows a software system to perceive its environment and rtake action that maximizes is chance of successfully achieving its goals, being able to adapt or learn something on its own.

First approach is employing *deep learning* that's modeled after a human minds neural network to self discover, learn and grow through experience.

Second approach is *machine learning*, which is a data science technique that uses existing data to train a model, test it and apply the model to new datato forecast behaviors, outcomes and trends.

Forecasting and predicting from machine learning can make devices / software smarter, like recommending products to you on an e-commerce platform based on your shopping history and others who've bought similar products.

## Azure Product Options

Azure offers three primary products designed for specific use-cases.

### Azure Machine Learning

A platform for making predictions and consists of tools and service that connects to data to train and test models. Once trained it can be deployed and used via web API endpoints.

* * Allows to define a process for obtaining data and handling missing/corrupted data, split it into a training set or test set and deliver it to the training process
* Use programming languages used by data scientists to train and evaluate predictive models
* Ability to create pipelines based on training / test data that define when and where to run the experiments to score the algorithm
* Deploy the algorithm as an API to be consumed in real time by other applications

Ideal when complete control over the design and training of an algorithm is required.

### Azure Cognitive Services

Prebuilt machine learning models that enable applications to see, hear, speak, understand and even begin to reason (*0*). Useful for solving general problems like analyzing text for emotional sentiment or images to recognize objects / faces with no knowledge of special machine learning or data science. Developers can include these features via an API in a few lines of code to use pretrained models on live data.

Azure Cognitive Services categories:

* Language services: Allows the process of natural language to evaluate sentiment to learn and recognize user wants via a prebuilt script
* Speech services: Convert speech to text and text to natural-sounding speech (scary), translation and speaker verification and recognition
* Vision services: Recognition and identification capabilities on images, videos and other visual content
* Decision services: Personalized recommendations for users that automatically improves through use, moderate and monitor content and remove derogatory content and abnormalities in time series data

### Azure Bot Service / Bot Framework

Platforms for creating virtual agents that understand and reply to questions just like a human.
( ͡ಠ ʖ̯ ͡ಠ)
Its use case is to create a virtual agent to communicate with humans using other Azure services like Azure Cognitive Services to understand what the human is asking. Put the bots to handle menial tasks (this is how the uprising begins) like taking a dinner reservations and automate the process.

## Analyze the Decision Criteria

### Are you building a virtual agent that interfaces with humans via natural language?

Use Azure Bot Service when a virtual agent is needed to interact with humans using natural language.

### Do you need a service that can understand the content and meaning of images, video, or audio, or that can translate text into a different language?

Use Azure Cognitive Services for general purpose tasks, like text to speech, integrating with search or object identification. Benefit from the work Microsoft already did to train and test the models needed.

### Will your app predict future outcomes based on private historical data?

Use Azure Machine Learning when data need analyzation for predicting future outcomes. Since you'll be working with proprietary data, you'll need to build custom-tailored models. With that...

### Do you need to build a model by using your own data or perform a different task than those listed above?

We use Azure Machine Learning as we have the greatest flexibility and engineers can use the tools they're familiar with to develop models needed.

# Choose the Best Azure Serverless Technology for your Business Scenario

_Serverless computing_ is a term used for an execution environment that is provisioned and managed by the provider.

## Identify the Product Options

With serverless computing there is no maintaining servers, configuring infrastructure and maintaining it is handled by the provider, like scaling and performance. Serverless apps are event-driven and they only run when triggered.

### Azure Functions

Host a single method/function by using a programming language (C#, Python, JavaScript, Java, Powershell) that runs on an event, like an HTTP request, message queue, or a timer.

Scales automatically and billed only when the function is triggered, which is great for variable demand. It is stateless and behaves as if restarted everytime it is triggered but can be stateful by connecting an Azure storage account to it, thus making it a **Durable Function**.

### Azure Logic Apps

Low-code/no-code development platform hosted as a cloud service. Covers app integration, data integration, system integration, enterprise application integration (EAI) and business-to-business (B2B) integration.

Designed in a web-based designer and executed by Azure services without writing code. Link triggers to action with connectors and you got yourself an app! 

* Trigger is an event
* Action is a task to execute

If there is no action or connector to your need you can always build your own, now you got to code!

### What are the differences between these services?

Azure Functions is a serverless compute server and Azure Logic Apps is a serverless orchestration service. Azure Functions can be used to orchestrate long-running business processes (Durable Function), that's not its primary use case when it was designed.

Azure Function is billed per execution and running time of each execution while Logic Apps is per execution and **type of connectors** it utitlizes.

## Analyze the Decision Criteria

### Do you need to perform an orchestration across well-known APIs?

Azure Logic Apps -- though you can do it with Azure Functions, it would take more time as you'd have to know what API's to use and orchestration was not its primary designed purpose.

### Do you need to execute custom algorithms or perform specialized data parsing and data lookups?

Azure Functions

### Do you have existing automated tasks written in an imperative programming language?

Azure Functions

# Choose the Best Tools to Help Organizations Build Better Solutions

Microsoft has a comprehensive set of tools to implement DevOps practices, solutions and save money.

## Understand Your Product Options

Software devs/operations pros create working software systems to meet the orgs needs but their short-term objectives can result in technical issues, delays and downtime.

Cue, DevOps, helps align technical teams as they work toward common goals by employing practices and processes to automate ongoing development, maintenance and deployment. Expedite releases and ensure changes are of exceptional quality.

DevOps practices touches on software development lifecycle, planning, project management, and collab with software devs/operations/and qa. **It's a fundamental mindset shift from the top down** not just installing some tools and be like DevOps baby! (͠≖ ͜ʖ͠≖)

### Product options

#### Azure DevOps Services

A suite of services that addresses every stage of the development lifecycle.

* **Azure Repos** is a source-code repository like GitHub/Bitbucket
* **Azure Boards** is an agile project management suite like JIRA
* **Azure Pipelines** is an automational tool for CI/CD like Jenkins/GitLab
* **Azure Artifacts** is a repo to host artifacts like JFrog's Artifactory
* **Azure Test Plans** is an automated test tool to ensure quality in the CI/CD pipeline like TestRail

Started off as an on-premises software and evolved to be a SaaS.

#### GitHub and GitHub Actions

Git is a decentralized source-code management tool and GitHub is the host version of Git serving as a primary remote.

* A shared source-code repository
* Facilitates project management
* Supports issue reporting, discussion and tracking
* Features CI/CD pipeline
* Includes a wiki for documentation
* Can be on-premises of in the cloud

GitHub Actions enables workflow automation with triggers for lifecycle events like automating a CI/CD _toolchain_.

> **Toolchain**  
> Combination of software tools that aid in the delivery, development and management of software applications throughout the development lifecycle

The output of one tool in the chain is the input for the next tool in the chain. 

So Azure DevOps or GitHub? Not a straightforward answer. GitHub is light-weight and trusted by thousands of open-source project owners, big focus on individual developers. Azure DevOps is more enterprise level, heavy on the project-management and planning tools with a more finer-grained access control. 

In the end you're not tied to one or the other, you can use GitHub for your repos and Azure Boards for your project management, mix-and-match baby!

#### Azure DevTest Labs

Provides an automated means of managing the process of building, setting up, and tearing down VMs containing build of software projects. Not limited to VMs, can be applied to anything deployed to Azure via an ARM template.

## Analyze the decision criteria

### Do you need to automate and manage test-lab creation?

Azure DevTest Labs, but can automate provisioning as part of a toolchain by using Azure Pipelines or Github Actions

### Are you building open-source software?

GitHub -- long been the preferred host for open-source though it can be done via public repos in Azure DevOps.

### Regarding source-code management and DevOps tools, what level of granularity do you need for permissions?

Github is a model of read/write permissions.
Azure DevOps is a set of granular permissions to refine who is able to perform operations across the tollset.

### Regarding source-code management and DevOps tools, how sophisticated does your project management and reporting need to be?

Azure DevOps is highly customizable which allows for the addition of custom fields to capture metadata and other information.

# Choose the Best Tools for Managing and Configuring Your Azure Environment

By using Azure maangement tools -- administrators, developers and managers can interact with the cloud environment to perform tasks like:

* Deploying dozens of hundreds of resources at a time
* Configuring individual services programmatically
* Viewing rich reports acorss usage, health, costs and more

## Identify the Product Options

Visual tools provide full, visually friendly access to all the functionality of Azure, not very useful when doing large deployments of resources with interdependencies and configurations options.

A code-based tool is better suited to quickly set up and configure Azure resources, as the commands and parameters used can be save into files for reusability. Another factor is the code can stored, versioned and maintained along with the source code in a source code repository. 

> **Infrastructure as Code**  
> Managing hardware and cloud resources via code

**Imperative code** details each step to be performed to achieve the desired outcome, whereas **declarative code** only details the desired outcome and the interpreter decides best approach to achieve it.

### Your Product Options

#### The Azure Portal

A web-based UI for accessing all the features of Azure, with a friendly graphical UI to view services used, services to create, service configuration and reports.

#### The Azure Mobile App

iOS and Android access to your Azure resources.

* Monitor the health and status of your Azure resources
* Check for alerts, quickly diagnose and fix issues and restart a web app or virtual machine (VM)
* Run the Azure CLI or Azure PowerShell commands to manage your Azure resources

#### Azure Powershell

A shell with which commands can be executed called cmdlets (command-lets). Invoking the Azure Rest API to perform management tasks within Azure which the cmdlets can be executed independently or part of a script (which can make the process automated/repeatable) to orchestrate:

* Routine setup, teardown and maintenance of a single resource or multiple connected resources
* Deployment of an entire infrastructure, which might have dozens/hundreds of imperative code resources

Available for Windows, Linux and macOS ヽ( ͡ಠ ʖ̯ ͡ಠ)ﾉ -- also accessible via the web browser using Azure Cloud Shell.

#### The Azure CLI

An executable program to execute commands in Bash ┏( ͡° ͜ʖ ͡°)┛ which call the Azure Rest API to perform management tasks within Azure. As with Azure Powershell the commands can be ran independently or in a script. 

Azure PowerShell and Azure CLI are identical in what they can do, it's just down to preference and what you already know.

#### ARM Templates

Imperative code can be written in Azure PowerShell / CLI for the provisioning. deprovisioning  and orchestration of resources but there exists a better method.

Azure Resource Manager (ARM templates) allow one to describe the resources wanted in a declarative JSON format. The template is verified before execution to validate resource creation and interconnectivity, which then orchestrates the creation of the resources in parallel. 

Just define the desired state and configuration for each resource and the template does the rest. PowerShell and Bash scripts can also be executed before or after a resource has been provisioned.

# Choose the Best Monitoring Service for Visibility, Insight and Outage Mitigation

Today's software running in the cloud is complex and wanting to see health and performance metrics across all of its layers can be challenging. Microsoft has just the solutions to be quick to react on outages, look into intermittent issues, optimize usage and be proactive in handling future downtime.

## Identify your Product Options

Several basic questions or concerns face all companies that use the cloud.

* Are we using the cloud correctly? Can we squeeze more performance out of our cloud spend?
* Are we spending more than we need to?
* Do we have our systems properly secured?
* How resilient are our resources? If we experience a regional outage, could we fail over to another region?
* How can we diagnose and fix issues that occur intermittently?
* How can we quickly determine the cause of an outage?
* How can we learn about planned downtime?

By using a combination of monitoring solutions on Azure, you can:

* Gain answers, insights, and alerts to help ensure that you've optimized your cloud usage.
* Ascertain the root cause of unplanned issues.
* Prepare ahead of time for planned outages.

### The Product Options

#### Azure Advisor

Evaluates Azure resources and makes recommendations to help improve reliability, security, performance, achieve operation excellence and reduce costs -- designed to help save time on cloud optimization.

Recommendations produced by Azure Advisor are available in the portal and the API. Notifcations can be set up to alert on new recommendations.

In the portal, Advisor dashboard displays personalized recommendations for all subscriptions and can be filtered by specific subscription, resource group or service; divided into five categories:

* Reliability: Used to ensure and improve the continuity of your business-critical applications.
* Security: Used to detect threats and vulnerabilities that might lead to security breaches.
* Performance: Used to improve the speed of your applications.
* Cost: Used to optimize and reduce your overall Azure spending.
* Operational Excellence: Used to help you achieve process and workflow efficiency, resource manageability, and deployment best practice

#### Azure Monitor

Platform for collecting, analyzing, visualizing and maybe taking action based on metric/logging data from Azure/on-premises environment.

<div align="center" style="min-width: 700px; background: #FFF; color: #000;">
	<img src="./assets/azure_monitor.png" />
	<p>
		<small>(⌐▀͡ ̯ʖ▀)</small>
	</p>
</div>

* On the left is a list of the sources of logging and metric data that can be collected at every layer in the application architecture, from application to operating system and network.
* In the center, logging and metric data is stored in central repositories.
* On the right, the data is used in a number of ways. View real-time and historical performance across each layer of the architecture, or aggregated and detailed information. Data is displayed at different levels for different audiences. View high-level reports on the Azure Monitor Dashboard or create custom views by using Power BI and Kusto queries.

Can have alerts delivered for critical events in real time through SMS, email and other methods.

Products like Azure Applucation Insights, which is a service for sending telemetry info from application source code to Azure, uses Azure Monitor under the hood. Application Insights allows developers to take advantage of powerful data-analysis in Azure Monitor to diagnose errors without waiting on users to report them.

#### Azure Service Health

Provides a personalized view of the Azure services, regions and resource the organization rely on. While status.azure.com displays major issues, Azure Service Health displays both major and minor issues which are localized.

Service Health helps you keep an eye on several event types:

* **Service issues** are problems in Azure, such as outages, that affect you right now. You can drill down to the affected services, regions, updates from your engineering teams, and find ways to share and track the latest information.
* **Planned maintenance** events can affect your availability. You can drill down to the affected services, regions, and details to show how an event will affect you and what you need to do. Most of these events occur without any impact to you and aren't shown here. In the rare case that a reboot is required, Service Health allows you to choose when to perform the maintenance to minimize the downtime.
* **Health advisories** are issues that require you to act to avoid service interruption, including service retirements and breaking changes. Health advisories are announced far in advance to allow you to plan.
