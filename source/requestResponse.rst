#####################
RANK API data request
#####################

For RANK API data extraction is accopmlished by referencing ``//blp/rankapi-beta``  as the service name in your program. This command will allow your service to redirect all RANK API request to the test environment.

Once the client has thoroughly tested the custom-built strategies, they can acces the service in production environment by changing the service name from ``//blp/rankapi-beta`` to  ``//blp/rankapi``.


Accessing the Test Environment
==============================
Bloomberg provides a test environment for clients to build and test their strategies using the IOI API.


API Demo Tool
=============
API Demo Tool is a handy tool while developing on any Bloomberg API services. The API Demo Tool provides real-time schema viewing tool among other handy tools that can be leveraged during the initial development.

The API Demo Tool can be downloaded from the Bloomberg terminal along with other generic Bloomberg API code samples.

    ``WAPI<GO>`` >> ``API Download Center`` >> ``Download`` 


Error Messages
==============

The following are the list of the Error messages from the RANK API service.


+----------------------------------------------+-------------------------------------------------------+
|Error Message                                 |Definition                                             |
+==============================================+=======================================================+
| No Start Date provided in RANK API request   |  Need to provide start date                           |
+----------------------------------------------+-------------------------------------------------------+
| No End Date provided in RANK API request     |  Need to provide end date                             |
+----------------------------------------------+-------------------------------------------------------+
| No units specified in RANK API request       |                                                       |
+----------------------------------------------+-------------------------------------------------------+
| No gropuBy specified in RANK API request     |                                                       |
+----------------------------------------------+-------------------------------------------------------+
| No source specified in RANK API request      |                                                       |
+----------------------------------------------+-------------------------------------------------------+
| Invalid request parameter                    | | Securities, exchanges or brokers need to be         |
|                                              | | specified in input query. At least one is required  |
+----------------------------------------------+-------------------------------------------------------+






