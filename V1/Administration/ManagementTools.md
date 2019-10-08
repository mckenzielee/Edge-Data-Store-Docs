---
uid: managementTools
---

# Edge Data Store management tools

## Command Line configuration

You can use the [edgecmd](xref:commandLine) utility on both Linux and Windows to configure and manage Edge Data Store.

## REST tools

The following tools are available to facilitate the execution of REST calls.

### cURL

Edge Data Store documentation displays cURL commands for configuration and management examples. cURL is a command line tool supported on Windows and Linux, used to make HTTP calls. cURL has a large range of capabilities: you can accomplish any Edge Data Store administrative or programming task with cURL. cURL is also easily scripted, using BASH or Powershell on either Linux or Windows. OSIsoft recommends this tool for managing Edge Data Store. Any system that can run Edge Data Store supports cURL.

### Postman

Postman is an effective REST tool for systems with GUI components (Edge Data Store is supported on platforms that lack this capability). It is particularly useful for learning more about Edge Data Store REST APIs.

### C#, Python, Go

You can use any modern programming language to make REST calls to administer and write programs for Edge Data Store. Since the administrative and programming interfaces are unified in using REST, you can write applications that both manage Edge Data Store and read and write data. If you want you can, for example, access the Diagnostics namespace locally to monitor and act upon the local system state.

### System Tools

Many OSIsoft customers use Windows computers, even though they may deploy Linux devices to host Edge Storage. You can install Edge Data Store on Windows 10, and the same custom applications developed on Windows should work on Linux, as long as the application development environment is supported on Linux. Edge Data Store has been designed to use platform independent programming. To facilitate working with Linux devices, Windows tools like PuTTY and WinSCP are very useful for copying files and remotely accessing Linux command lines.
