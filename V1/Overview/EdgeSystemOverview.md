---
uid: EdgeDataStoreOverview
---

# Overview

Edge Data Store (EDS) is an embedded data server that runs on Linux and Windows. EDS is a supplement to existing OSIsoft products. It is designed for small devices, and you can install and run it on 64-bit Intel/AMD compatible and 32-bit ARM v7/v8 compatible chips. It offers REST programming, configuration, administrative interfaces, and a command line tool that you use to configure and administer EDS. EDS provides a means of ingressing data from a variety of devices and applications into the PI System or OCS.

EDS does not offer any built-in visualization or analytic support; however, if you use the REST programming capabilities built into EDS, you can write analytics or visualization programs on either Linux, Windows, or both in a variety of programming languages.

## Edge Data Store architecture
The following diagram depicts the relationships of architectural components to one another in the Edge Data Store:

![EDS architecture](https://osisoft.github.io/Edge-Data-Store-Docs/V1/images/EDSArchitecture.jpg "EDS architecture")

## Edge Data Store data flow
The following diagram depicts the flow of data in the Edge Data Store:

![EDS data flow](https://osisoft.github.io/Edge-Data-Store-Docs/V1/images/EDSOverview1.jpg "EDS data flow")

## Edge Data Store components
The following diagram depicts the relationship of key functions to relevant components of the Edge Data Store:

![EDS components](https://osisoft.github.io/Edge-Data-Store-Docs/V1/images/EDSOverview2.jpg "EDS components")

## Edge Data Store installation

You can install Edge Data Store on both Linux and Windows. For more information see [Installation](xref:installationOverview).

## Data ingress to Edge Data Store

Edge Data Store can ingress data in a number of ways. There are two built-in adapters: [EDS Modbus TCP](xref:modbusQuickStart) and [EDS OPC UA](xref:opcUaQuickStart). Data can also be ingressed using OSIsoft Message Format [(OMF)](xref:omfQuickStart) and the Sequential Data Store [SDS](xref:sdsWritingData) REST APIs.

The following diagram depicts an OMF data ingress scenario in the Edge Data Store:

![EDS OMF Ingress](https://osisoft.github.io/Edge-Data-Store-Docs/V1/images/EDSOMFIngress.jpg "EDS OMF Ingress")

During installation of Edge Data Store, you can choose to install either an EDS Modbus TCP adapter or an EDS OPC UA adapter, or both. The EDS Modbus and EDS OPC UA adapters require configuration of data source and data selection before they can collect data in Edge Data Store. You can use OMF data ingress once Edge Data Store is installed, with no further configuration steps.

Edge Data Store is composed of components, and is designed to allow additional EDS adapters at a later point.


## Local data read and write access

You can access all data in Edge Data Store by using the Sequential Data Store [SDS Read/Write quick start](xref:sdsQuickStart) REST API. You can use this data for local applications that perform analytics or visualization. 

### Example EDS visualization application
The following diagram depicts the flow of data from a customer visualization application into Edge Data Store, via either OMF or SDS REST calls:

![EDS Visualization](https://osisoft.github.io/Edge-Data-Store-Docs/V1/images/EDSVisualization.jpg "EDS Visualization")

### Example EDS analytics application
The following diagram depicts the flow of data from a customer analytics application into Edge Data Store, via either OMF or SDS REST calls:

![EDS Analytics](https://osisoft.github.io/Edge-Data-Store-Docs/V1/images/EDSAnalytics.jpg "EDS Analytics")

## Data egress from Edge Data Store

Edge Data Store can send data to both PI Data Archive using PI Web API and OSIsoft Cloud Services. For more information, see [PI egress quick start](xref:piEgressQuickStart) and [OCS egress quick start](xref:ocsEgressQuickStart).

After Edge Data Store is installed, additional configuration is necessary to send data to both OCS and PI Web API.
