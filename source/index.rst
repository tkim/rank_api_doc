.. RANK API Programmers Guide documentation master file, created by
   sphinx-quickstart on Mon Jan 20 16:37:19 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

##########################
RANK API Programmers Guide
##########################

This document is for developers who will use the Bloomberg RANK API Server to request RANK data from Bloomberg.

The RANK API allows clients to use Bloomberg API 3.0 to automate the RANK API data extract from Bloomberg to clients application.

The Bloomberg API uses an event-driven model. The RANK API is an extension of Bloomberg API 3.0 and it lets users integrate streaming real-time and static data into their own custom applications. The user can choose the data they require down to the level of individual fields. The Bloomberg API 3.0 programming interface implementations are extremely lightweight. For details to the Desktop and Server API, please refer to the  API Programmers Guide from ``WAPI<GO>`` in your Bloomberg terminal.

The Bloomberg API interface is thread-safe and thread-aware, giving applications the ability to utilize multiple processors efficiently. The Bloomberg API supports run-time downloadable schema for the service it provides, and it provides methods to query these schemas at runtime. This means additional service in Bloomberg API is supported without addition to the interface.

The object model for Java, .NET and C++ are identical. The C interface provides a C-style version of the object model.


.. warning::
	
	Please note that performance/load test should never be performed on any of the API environment as this is a shared environment and we monitor and increase capacity as needed.




.. toctree::
   :maxdepth: 2
   
   introduction
   serverApi
   requestResponse
   

