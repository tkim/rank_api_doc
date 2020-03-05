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

BLP API Infrastrcuture related error messages:-

+----------------------------------------------+-------------------------------------------------------+
|Error Message                                 |Definition                                             |
+==============================================+=======================================================+
| ... BLPAPI Timeout event ...                 | | Set sessionOption.setMaxPendingRequest(1). Do not   |
|                                              | | have multiple sessions in parallel with the same    |
|                                              | | UUID.                                               |
+----------------------------------------------+-------------------------------------------------------+

Rank API service error messages:-

+----------------------------------------------+-------------------------------------------------------+
|Error Message                                 |Definition                                             |
+==============================================+=======================================================+
| No Start Date provided in RANK API request   |  Mandatory field, need to provide the start date      |
+----------------------------------------------+-------------------------------------------------------+
| No End Date provided in RANK API request     |  Mandatory field, need to provide end date            |
+----------------------------------------------+-------------------------------------------------------+
| No units specified in RANK API request       | | Mandatory field, need to specify units              |
|                                              | | (e.g. Shares, Local, USD, EUR, GBP)                 |
+----------------------------------------------+-------------------------------------------------------+
| No gropuBy specified in RANK API request     | | Mandatory field, need to specify groupby element    |
|                                              | | (e.g. broker or security)                           |
+----------------------------------------------+-------------------------------------------------------+
| No source specified in RANK API request      | | Mandatory field, need to specify the source element |
|                                              | | (e.g. Broker Contributed)                           |
+----------------------------------------------+-------------------------------------------------------+
| | Source field invalid. Only source =        | The source field has invalid input value.             |
| | BROKER_CONTRIBUTED is supported            |                                                       |  
+----------------------------------------------+-------------------------------------------------------+
| Invalid unit value                           | The unit field has invalid input value.               |
+----------------------------------------------+-------------------------------------------------------+
| Invalid groupby value                        | | The groupby field has invalid input value.          |
|                                              | | (e.g. broker or security)                           |
+----------------------------------------------+-------------------------------------------------------+
| Invalid start date                           | The start date parameter contains invalid input.      |
+----------------------------------------------+-------------------------------------------------------+
| Invalid end date                             | The end date parameter contains invalid input.        |
+----------------------------------------------+-------------------------------------------------------+
| Invalid security selection                   | Neither ticker nor figi was provided.                 |
+----------------------------------------------+-------------------------------------------------------+
| Invalid request parameters                   | | Invalid request. The result contains multiple       |
|                                              | | exchanges or no securities, exchanges or brokers are|
|                                              | | specified in the request.                           |
+----------------------------------------------+-------------------------------------------------------+
| | Invalid broker list include/exclude        | | Invalid combination of included or excluded broker  |
| | combination.                               | | list.                                               |
+----------------------------------------------+-------------------------------------------------------+
| End date less than start date                | | The start date/time should be earlier in date/time  |
|                                              | | compared to the end date/time.                      |
+----------------------------------------------+-------------------------------------------------------+
| | Start date less than earliest allowed date | | The start date/time should be within 5 years from   | 
| | for RANK query                             | | the current date.                                   |
+----------------------------------------------+-------------------------------------------------------+
| No ticker conversion for figi                | | The figi provided did not find a corresponding      |
|                                              | | ticker value.                                       |
+----------------------------------------------+-------------------------------------------------------+
| Internal Error                               | | Please contact Bloomberg, miscellaneous error.      |
+----------------------------------------------+-------------------------------------------------------+


RANK API Code Samples
=====================

.. important::

			The latest RANK API Code samples can be found `here`_.

			.. _here: https://github.com/tkim/rank_api_repository







