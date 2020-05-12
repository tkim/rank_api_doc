#####################
RANK API data request
#####################

For RANK API data extraction is accopmlished by referencing ``//blp/rankapi-beta``  as the service name in your program. This command will allow your service to redirect all RANK API request to the test environment.

Once the client has thoroughly tested the custom-built strategies, they can acces the service in production environment by changing the service name from ``//blp/rankapi-beta`` to  ``//blp/rankapi``.

.. important::

	Please keep each request to have less than 3000 securities per request.


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

+-------------------------------------------+-------------------------------------------------------+
|Error Message                              |Definition                                             |
+===========================================+=======================================================+
| ... BLPAPI Timeout event ...              | | Set sessionOption.setMaxPendingRequest(1). Do not   |
|                                           | | have multiple sessions in parallel with the same    |
|                                           | | UUID.                                               |
+-------------------------------------------+-------------------------------------------------------+

Rank API service error messages:-

+-------------------------------------------+----------+-------------------------------------------------------+
|Error Message                              |Error Code|Definition                                             |
+===========================================+==========+=======================================================+
| | No Start Date provided in RANK API      | 99       | | Mandatory field, need to provide the start date     |
| | request                                 |          |                                                       |
+-------------------------------------------+----------+-------------------------------------------------------+
| | No End Date provided in RANK API        | 99       | | Mandatory field, need to provide end date           |
| | request                                 |          |                                                       |
+-------------------------------------------+----------+-------------------------------------------------------+
| | No units specified in RANK API          | 99       | | Mandatory field, need to specify units              |
| | request                                 |          | | (e.g. Shares, Local, USD, EUR, GBP)                 |
+-------------------------------------------+----------+-------------------------------------------------------+
| | No gropuBy specified in RANK API        | 99       | | Mandatory field, need to specify groupby element    |
| | request                                 |          | | (e.g. broker or security)                           |
+-------------------------------------------+----------+-------------------------------------------------------+
| | No source specified in RANK API         | 99       | | Mandatory field, need to specify the source element |
| | request                                 |          | | (e.g. Broker Contributed)                           |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Source field invalid. Only source =     | 28       | | The source field has invalid input value.           |
| | BROKER_CONTRIBUTED is supported         |          |                                                       |  
+-------------------------------------------+----------+-------------------------------------------------------+
| | Invalid unit value                      | 20       | | The unit field has invalid input value.             |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Invalid groupby value                   | 21       | | The groupby field has invalid input value.          |
|                                           |          | | (e.g. broker or security)                           |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Invalid start date                      | 22       | | The start date parameter contains invalid input.    |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Invalid end date                        | 23       | | The end date parameter contains invalid input.      |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Invalid security selection              | 27       | | Neither ticker nor figi was provided.               |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Invalid request parameters              | 1        | | Invalid request. The result contains multiple       |
|                                           |          | | exchanges or no securities, exchanges or brokers are|
|                                           |          | | specified in the request.                           |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Invalid broker list include/exclude     | 5        | | Invalid combination of included or excluded broker  |
| | combination.                            |          | | list.                                               |
+-------------------------------------------+----------+-------------------------------------------------------+
| End date less than start date             | 24       | | The start date/time should be earlier in date/time  |
|                                           |          | | compared to the end date/time.                      |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Start date less than earliest allowed   | 25       | | The start date/time should be within 5 years from   | 
| | date for RANK query                     |          | | the current date.                                   |
+-------------------------------------------+----------+-------------------------------------------------------+
| | No ticker conversion for figi           | 26       | | The figi provided did not find a corresponding      |
|                                           |          | | ticker value.                                       |
+-------------------------------------------+----------+-------------------------------------------------------+
| | Internal Error                          | Various  | | Please contact Bloomberg, miscellaneous error.      |
+-------------------------------------------+----------+-------------------------------------------------------+


Description of Elements
=======================
The following elements are available for RANK API.

+------------------------------+-----------------------------------------------+---------+
|Element Name                  | Description                                   | Type    |
+==============================+===============================================+=========+
|``acronym``                   | Broker acronym / IPER code                    | string  |
+------------------------------+-----------------------------------------------+---------+
|``bought``                    | Number of bought                              | float64 |
+------------------------------+-----------------------------------------------+---------+
|``crossed``                   | Number of crossed                             | float64 |
+------------------------------+-----------------------------------------------+---------+
|``errorCode``                 | Error code                                    | int32   |
+------------------------------+-----------------------------------------------+---------+
|``errorMessage``              | Error Message                                 | string  |
+------------------------------+-----------------------------------------------+---------+
|``figi``                      | Security identifier as figi                   | string  |
+------------------------------+-----------------------------------------------+---------+
|``highTouch``                 | Number of high touch orders                   | float64 |
+------------------------------+-----------------------------------------------+---------+
|``lowTouch``                  | Number of low touch orders                    | float64 |
+------------------------------+-----------------------------------------------+---------+
|``numReports``                | Number of numReport                           | int32   |
+------------------------------+-----------------------------------------------+---------+
|``rank``                      | Broker rank                                   | int32   |
+------------------------------+-----------------------------------------------+---------+
|``ticker``                    | security identifier as Bloomberg ticker       | string  |
+------------------------------+-----------------------------------------------+---------+
|``sold``                      | Number of sold                                | float64 |
+------------------------------+-----------------------------------------------+---------+
|``timestampUtc``              | Timestampe in UTC                             | DateTime|
+------------------------------+-----------------------------------------------+---------+
|``total``                     | Number of high touch orders                   | float64 |
+------------------------------+-----------------------------------------------+---------+
|``traded``                    | Number of high touch orders                   | float64 |
+------------------------------+-----------------------------------------------+---------+




RANK Data request
=================
The ``rankDataRequest`` request allows RANK API service to pull the RANK data.

Full code sample:-

======================= =====================
`rankDataRequest cs`_   `rankDataRequest py`_
----------------------- ---------------------  
`rankDataRequest java`_
======================= =====================

.. _rankDataRequest cs: https://github.com/tkim/rank_api_repository/blob/master/RankAPI_C%23/rankDataRequest.cs
.. _rankDataRequest java: https://github.com/tkim/rank_api_repository/blob/master/RankAPI_Java/RankDataRequest.java
.. _rankDataRequest py: https://github.com/tkim/rank_api_repository/blob/master/RankAPI_Python/rankDataRequest.py


.. code-block:: python

	Bloomberg - RANK API Example - rankDataRequst
	Connecting to localhost:8194
	processEvent
	SessionConnectionUp = {
			server = "localhost:8194"
			encryptionStatus = "Clear"
	}

	Processing SESSION_STATUS eventReq
	SessionConnectionUp = {
			server = "localhost:8194"
			encryptionStatus = "Clear"
	}

	processEvent
	SessionStarted = {
			initialEndpoints[] = {
					initialEndpoints = {
							address = "localhost:8194"
					}
			}
	}

	Processing SESSION_STATUS event
	Session started...
	processEvent
	ServiceOpened = {
			serviceName = "//blp/rankapi-beta"
	}

	Processing SERVICE_STATUS event
	Service opened...
	Sending Request: Query = {
			brokers[] = {
					brokers = {
							acronym = "ABCD" #broker acronym
					}
			}
			start = 2020-02-01
			end = 2020-02-12
			groupBy = Broker
			securityCriteria = {
					exchanges[] = {
							exchanges = {
									code = "US"
							}
					}
			}
			source = Broker Contributed
			units = Shares
	}

	RANK data request sent.


Output:-

.. code-block:: python

	processEvent
	Report = {
			records[] = {
					records = {
							security = {
									ticker = "F US EQUITY"
							}
							topBrokers[] = {
									topBrokers = {
											acronym = "VIRT"
											name = "VIRTU FINANCIAL"
											rank = 1
									}
									topBrokers = {
											acronym = "CSFB"
											name = "CREDIT SUISSE"
											rank = 2
									}
							}
							bought = 0.000000
							sold = 0.000000
							traded = 27931645.000000
							crossed = 111154.000000
							total = 28153953.000000
							highTouch = 0.000000
							lowTouch = 0.000000
							numReports = 750
							}
							records = {
									security = {
											ticker = "CHK US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "VIRT"
													name = "VIRTU FINANCIAL"
													rank = 1
											}
											topBrokers = {
													acronym = "CSFB"
													name = "CREDIT SUISSE"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 22572462.000000
									crossed = 0.000000
									total = 22572462.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 434
							}
							records = {
									security = {
											ticker = "NOK US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "VIRT"
													name = "VIRTU FINANCIAL"
													rank = 1
											}
											topBrokers = {
													acronym = "CSFB"
													name = "CREDIT SUISSE"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 18260262.000000
									crossed = 0.000000
									total = 18260262.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 301
							}
							records = {
									security = {
											ticker = "GE US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "VIRT"
													name = "VIRTU FINANCIAL"
													rank = 1
											}
											topBrokers = {
													acronym = "CSFB"
													name = "CREDIT SUISSE"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 14989980.000000
									crossed = 0.000000
									total = 14989980.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 278
							}
							records = {
									security = {
											ticker = "PBR US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "MLCO"
													name = "MERRILL LYNCH"
													rank = 1
											}
											topBrokers = {
													acronym = "CSFB"
													name = "CREDIT SUISSE"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 14962016.000000
									crossed = 0.000000
									total = 14962016.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 317
							}
							records = {
									security = {
											ticker = "NLOK US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "BCAP"
													name = "BARCLAYS CAPITAL"
													rank = 1
											}
											topBrokers = {
													acronym = "MSCO"
													name = "MORGAN STANLEY"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 12741007.000000
									crossed = 100000.000000
									total = 12941007.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 505
							}
							records = {
									security = {
											ticker = "ABEV US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "CITI"
													name = "CITIGROUP GLOBAL MARKETS"
													rank = 1
											}
											topBrokers = {
													acronym = "VIRT"
													name = "VIRTU FINANCIAL"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 12476275.000000
									crossed = 0.000000
									total = 12476275.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 370
							}
							records = {
								security = {
										ticker = "INDL US EQUITY"
								}
								topBrokers[] = {
										topBrokers = {
												acronym = "VIRT"
												name = "VIRTU FINANCIAL"
												rank = 1
										}
										topBrokers = {
												acronym = "CSFB"
												name = "CREDIT SUISSE"
												rank = 2
										}
								}
								bought = 0.000000
								sold = 0.000000
								traded = 2200.000000
								crossed = 0.000000
								total = 2200.000000
								highTouch = 0.000000
								lowTouch = 0.000000
								numReports = 2
						}
				}
				timestampUtc = 2020-04-20T13:07:25.168+00:00
		}	


Request created specifying the ticker ``AAPL US Equity``:-

.. code-block:: python

	Bloomberg - RANK API Example - rankDataRequst
	Connecting to localhost:8194
	Processing SESSION_STATUS event
	SessionConnectionUp = {
		server = "localhost:8194"
		encryptionStatus = "Clear"
	}

	Processing SESSION_STATUS event
	Session started...
	Processing SERVICE_STATUS event
	Service opened...
	Sending Request: Query = {
		start = 2020-02-01
		end = 2020-02-12
		groupBy = Broker
		securityCriteria = {
			securities[] = {
				securities = {
					ticker = "AAPL US Equity"
				}
			}
		}
		source = Broker Contributed
		units = Shares
	}

	RANK data request sent.


Output:-

.. code-block:: python

	Processing RESPONSE event
	MESSAGE TYPE: Report
	records[] = {
		records = {
			broker = {
				acronym = "VIRT"
				name = "VIRTU FINANCIAL"
				rank = 1
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 34867000.000000
			crossed = 451500.000000
			total = 35770000.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 785
		}
		records = {
			broker = {
				acronym = "CSFB"
				name = "CREDIT SUISSE"
				rank = 2
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 14889257.000000
			crossed = 0.000000
			total = 14889257.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 177
		}
		records = {
			broker = {
				acronym = "MSCO"
				name = "MORGAN STANLEY"
				rank = 3
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 12007367.000000
			crossed = 0.000000
			total = 12007367.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 531
		}
		records = {
			broker = {
				acronym = "UBS"
				name = "UBS INVESTMENT BANK"
				rank = 4
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 11404285.000000
			crossed = 2197.000000
			total = 11408679.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 16
		}
		records = {
			broker = {
				acronym = "JPM"
				name = "JP MORGAN"
				rank = 5
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 8073579.000000
			crossed = 0.000000
			total = 8073579.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 774
		}
		records = {
			broker = {
				acronym = "SUSQ"
				name = "SUSQUEHANNA INTERNATIONAL GRP"
				rank = 6
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 5476600.000000
			crossed = 0.000000
			total = 5476600.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 108
		}
		records = {
			broker = {
				acronym = "MLCO"
				name = "MERRILL LYNCH"
				rank = 7
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 5253766.000000
			crossed = 0.000000
			total = 5253766.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 911
		}
		records = {
			broker = {
				acronym = "GS"
				name = "GOLDMAN SACHS & CO."
				rank = 8
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 4234509.000000
			crossed = 58167.000000
			total = 4350843.000000
			highTouch = 3407300.000000
			lowTouch = 943543.000000
			numReports = 789
		}
		records = {
			broker = {
				acronym = "CITI"
				name = "CITIGROUP GLOBAL MARKETS"
				rank = 9
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 3302578.000000
			crossed = 0.000000
			total = 3302578.000000
			highTouch = 1833230.000000
			lowTouch = 1469348.000000
			numReports = 22
		}
		records = {
			broker = {
				acronym = "BCAP"
				name = "BARCLAYS CAPITAL"
				rank = 10
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 2824156.000000
			crossed = 0.000000
			total = 2824156.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 150
		}
		records = {
			broker = {
				acronym = "INCA"
				name = "INSTINET"
				rank = 11
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 2406000.000000
			crossed = 0.000000
			total = 2406000.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 38
		}
		records = {
			broker = {
				acronym = "JEFF"
				name = "JEFFERIES & CO., INC."
				rank = 12
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 953536.000000
			crossed = 0.000000
			total = 953536.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 43
		}
		records = {
			broker = {
				acronym = "RBC"
				name = "ROYAL BANK OF CANADA"
				rank = 13
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 834355.000000
			crossed = 0.000000
			total = 834355.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 229
		}
		records = {
			broker = {
				acronym = "BERN"
				name = "SANFORD C. BERNSTEIN"
				rank = 19
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 211458.000000
			crossed = 0.000000
			total = 211458.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 18
		}
		records = {
			broker = {
				acronym = "PIPR"
				name = "PIPER JAFFRAY & CO."
				rank = 20
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 185400.000000
			crossed = 0.000000
			total = 185400.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 18
		}
		records = {
			broker = {
				acronym = "AGCO"
				name = "AUERBACH GRAYSON COMPANY INC"
				rank = 83
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 31.000000
			crossed = 0.000000
			total = 31.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
	}

	

RANK API Code Samples
=====================

.. important::

			The latest RANK API Code samples can be found `here`_.

			.. _here: https://github.com/tkim/rank_api_repository







