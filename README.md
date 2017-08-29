# Repo DotNet-Wksp1
# This is  a PCF .NET Demo involves multiple frameworks
This solution demonstrates the use of multiple microservices built using multiple .NET technologies and running on PCF. The primary goal is to show that PCF can handle legacy code that existed as early as .NET version 1.0, with common stacks introduced as part of .NET framework up to the newest .NET core application. The solution demonstrates a natural progression / evolution that a customer would take towards making their apps cloud native.

Technical Features Demonstrated:
- Running WebForms application
- Use of ASMX services
- WCF service connectivity
- OWIN bootstrap into IIS
- .NET core MVC application on Linux stack
- Service discovery via Eureka (using ASMX, WCF, and REST)
- MySQL connectivity using EntityFramework
- Config server with GIT repo

# Solution Projects
The solution revolves around a simple application that displays random quotes when a button is pressed. It also features a Kill command to simulate application failure.
* FortunesFormsUI - Web forms GUI. Depends on Eureka and Config Server. Depending on config value served by Config Server, the source of the messages shown will be switched between local in memory, ASMX service, WCF service, or REST
* ForunesLegacyService - Contains ASMX service and WCF service implementations for serving messages
   * ASMX fetches it's data from database connectivity via classic DataSet / DataAdapter approach
   * WCF featches data from database using a more modern approach using entity Framework
* FortunesServices - Rest based implementation using OWIN with WebAPI. Intended to be run on Windows stack with HWC
* FortunesUI - Modern .NET core version running on linux stack. Calls backend services directly from javascript.

![Architecture](Docs/project_architecture.png "Architecture")


# How to build
Run `\build\build.ps1`. The output will be dropped into `\publish\`
### Prerequisites
* Visual Studio 2017 with .NET core support

# How to deploy

* *Ensure that you have CF CLI as part of path, logged in, and targeting space/org where you want to deploy*

1. Run build\create-services.bat. Wait for services to finish being created (`cf services`)
2. Do `cf push` inside `\publish\` folder



# Resources
**Slides:** https://goo.gl/RfFZQd
**Config Repo:** https://github.com/reagul/fortunesconfig
