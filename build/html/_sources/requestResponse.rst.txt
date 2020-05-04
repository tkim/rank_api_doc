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


RANK Data request
=================


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
											ticker = "VXX US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "VIRT"
													name = "VIRTU FINANCIAL"
													rank = 1
											}
											topBrokers = {
													acronym = "ABCD"
													name = "ABCD CAPITAL"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 15629883.000000
									crossed = 0.000000
									total = 15629883.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 295
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
											ticker = "EEM US EQUITY"
									}
									topBrokers[] = {
											topBrokers = {
													acronym = "VIRT"
													name = "VIRTU FINANCIAL"
													rank = 1
											}
											topBrokers = {
													acronym = "CITI"
													name = "CITIGROUP GLOBAL MARKETS"
													rank = 2
											}
									}
									bought = 0.000000
									sold = 0.000000
									traded = 13579058.000000
									crossed = 0.000000
									total = 13579058.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 361
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
											ticker = "NIO US EQUITY"
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
									traded = 12397212.000000
									crossed = 0.000000
									total = 12397212.000000
									highTouch = 0.000000
									lowTouch = 0.000000
									numReports = 317
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
				acronym = "ITGI"
				name = "INVESTMENT TECHNOLOGY GROUP"
				rank = 14
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 343927.000000
			crossed = 700.000000
			total = 345327.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 325
		}
		records = {
			broker = {
				acronym = "HSBC"
				name = "HSBC GROUP PLC"
				rank = 15
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 303222.000000
			crossed = 0.000000
			total = 303222.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 5
		}
		records = {
			broker = {
				acronym = "WELS"
				name = "WELLS FARGO SECURITIES"
				rank = 16
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 285496.000000
			crossed = 1253.000000
			total = 288002.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 116
		}
		records = {
			broker = {
				acronym = "COWN"
				name = "COWEN & COMPANY"
				rank = 17
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 280654.000000
			crossed = 0.000000
			total = 280654.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 11
		}
		records = {
			broker = {
				acronym = "RAJA"
				name = "RAYMOND JAMES & ASSOCIATES"
				rank = 18
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 242873.000000
			crossed = 0.000000
			total = 242873.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 77
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
				acronym = "OPCO"
				name = "OPPENHEIMER & CO."
				rank = 21
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 168897.000000
			crossed = 0.000000
			total = 168897.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 135
		}
		records = {
			broker = {
				acronym = "BMOC"
				name = "BMO CAPITAL MARKETS"
				rank = 22
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 165772.000000
			crossed = 0.000000
			total = 165772.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 2
		}
		records = {
			broker = {
				acronym = "CIST"
				name = "CAPITAL INSTITUTIONAL SERVICES"
				rank = 23
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 115000.000000
			crossed = 0.000000
			total = 115000.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 23
		}
		records = {
			broker = {
				acronym = "BARD"
				name = "BAIRD (ROBERT W.) & CO., INC."
				rank = 24
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 99034.000000
			crossed = 11.000000
			total = 99056.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 15
		}
		records = {
			broker = {
				acronym = "ISI"
				name = "EVERCORE GROUP L.L.C."
				rank = 25
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 96000.000000
			crossed = 0.000000
			total = 96000.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 4
		}
		records = {
			broker = {
				acronym = "JONE"
				name = "JONESTRADING"
				rank = 26
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 83758.000000
			crossed = 0.000000
			total = 83758.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 4
		}
		records = {
			broker = {
				acronym = "KEPL"
				name = "KEPLER CAPITAL MARKETS"
				rank = 27
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 83143.000000
			crossed = 0.000000
			total = 83143.000000
			highTouch = 11582.000000
			lowTouch = 71561.000000
			numReports = 9
		}
		records = {
			broker = {
				acronym = "STFL"
				name = "STIFEL NICOLAUS COMPANY, INC."
				rank = 28
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 74444.000000
			crossed = 0.000000
			total = 74444.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 29
		}
		records = {
			broker = {
				acronym = "CANT"
				name = "CANTOR FITZGERALD L.P."
				rank = 29
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 70000.000000
			crossed = 0.000000
			total = 70000.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 7
		}
		records = {
			broker = {
				acronym = "WINS"
				name = "WINTERFLOOD SECURITIES"
				rank = 30
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 67588.000000
			crossed = 0.000000
			total = 67588.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 5
		}
		records = {
			broker = {
				acronym = "LQNT"
				name = "LIQUIDNET, INC"
				rank = 31
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 57382.000000
			crossed = 4400.000000
			total = 66182.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "MIZS"
				name = "MIZUHO SECURITIES"
				rank = 32
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 60663.000000
			crossed = 0.000000
			total = 60663.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 274
		}
		records = {
			broker = {
				acronym = "PEEL"
				name = "PEEL HUNT LLP"
				rank = 33
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 56566.000000
			crossed = 0.000000
			total = 56566.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "MACQ"
				name = "MACQUARIE SECURITIES"
				rank = 34
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 54635.000000
			crossed = 0.000000
			total = 54635.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 8
		}
		records = {
			broker = {
				acronym = "LOOP"
				name = "LOOP CAPITAL MARKETS"
				rank = 35
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 45993.000000
			crossed = 0.000000
			total = 45993.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 11
		}
		records = {
			broker = {
				acronym = "JSSF"
				name = "JMP SECURITIES LLC"
				rank = 36
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 43747.000000
			crossed = 0.000000
			total = 43747.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "BTIG"
				name = "BTIG LLC"
				rank = 37
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 33935.000000
			crossed = 0.000000
			total = 33935.000000
			highTouch = 33935.000000
			lowTouch = 0.000000
			numReports = 5
		}
		records = {
			broker = {
				acronym = "SG"
				name = "SG SECURITIES"
				rank = 38
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 33399.000000
			crossed = 0.000000
			total = 33399.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 17
		}
		records = {
			broker = {
				acronym = "CICC"
				name = "CHINA INTERNATIONAL CAPITAL CO"
				rank = 39
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 31700.000000
			crossed = 0.000000
			total = 31700.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 2
		}
		records = {
			broker = {
				acronym = "DAIW"
				name = "DAIWA SECURITIES INC."
				rank = 40
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 31600.000000
			crossed = 0.000000
			total = 31600.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "KBCE"
				name = "KBC SECURITIES"
				rank = 41
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 30868.000000
			crossed = 0.000000
			total = 30868.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 5
		}
		records = {
			broker = {
				acronym = "KEYB"
				name = "KEYBANC CAPITAL MARKETS"
				rank = 42
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 30722.000000
			crossed = 0.000000
			total = 30722.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 8
		}
		records = {
			broker = {
				acronym = "XP"
				name = "XP SECURITIES LLC"
				rank = 43
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 30150.000000
			crossed = 0.000000
			total = 30150.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 15
		}
		records = {
			broker = {
				acronym = "KBWI"
				name = "KEEFE, BRUYETTE & WOODS, INC."
				rank = 44
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 24340.000000
			crossed = 0.000000
			total = 24340.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "WBLR"
				name = "WILLIAM BLAIR & COMPANY"
				rank = 45
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 23652.000000
			crossed = 0.000000
			total = 23652.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "EXNE"
				name = "EXANE"
				rank = 46
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 23245.000000
			crossed = 0.000000
			total = 23245.000000
			highTouch = 23245.000000
			lowTouch = 0.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "DBAB"
				name = "DEUTSCHE BANK SECURITIES INC"
				rank = 47
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 22743.000000
			crossed = 0.000000
			total = 22743.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 8
		}
		records = {
			broker = {
				acronym = "VTB"
				name = "VTB BANK"
				rank = 48
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 22150.000000
			crossed = 0.000000
			total = 22150.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "STRS"
				name = "STRATEGAS RESEARCH PARTNERS"
				rank = 49
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 20968.000000
			crossed = 0.000000
			total = 20968.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "ANOS"
				name = "ABEL / NOSER CORP"
				rank = 50
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 19920.000000
			crossed = 0.000000
			total = 19920.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 11
		}
		records = {
			broker = {
				acronym = "BIDS"
				name = "BIDS HOLDINGS, L.P."
				rank = 51
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 0.000000
			crossed = 8900.000000
			total = 17800.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "MAKR"
				name = "MAKOR CAPITAL LTD"
				rank = 52
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 12151.000000
			crossed = 0.000000
			total = 12151.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 2
		}
		records = {
			broker = {
				acronym = "LCUK"
				name = "LOUIS CAPITAL MARKETS, LP"
				rank = 53
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 11324.000000
			crossed = 0.000000
			total = 11324.000000
			highTouch = 11324.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "WLFE"
				name = "WOLFE RESEARCH SECURITIES"
				rank = 54
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 10399.000000
			crossed = 0.000000
			total = 10399.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "SSCO"
				name = "SAFRA SECURITIES LLC"
				rank = 55
			}
			topBrokers[] = {
			}
			bought = 8780.000000
			sold = 1000.000000
			traded = 9780.000000
			crossed = 0.000000
			total = 9780.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "ING"
				name = "ING BANK"
				rank = 56
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 8516.000000
			crossed = 0.000000
			total = 8516.000000
			highTouch = 0.000000
			lowTouch = 8516.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "INTL"
				name = "INTL TRADING INC"
				rank = 57
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 7613.000000
			crossed = 0.000000
			total = 7613.000000
			highTouch = 351.000000
			lowTouch = 0.000000
			numReports = 10
		}
		records = {
			broker = {
				acronym = "INSG"
				name = "INTERSTATE GROUP, THE"
				rank = 58
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 7253.000000
			crossed = 0.000000
			total = 7253.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "MNFB"
				name = "MAIN FIRST BANK AG"
				rank = 59
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 6802.000000
			crossed = 0.000000
			total = 6802.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 4
		}
		records = {
			broker = {
				acronym = "SBER"
				name = "SBERBANK CIB CJSC"
				rank = 60
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 6770.000000
			crossed = 0.000000
			total = 6770.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "CICS"
				name = "CM-CIC SECURITIES"
				rank = 61
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 6521.000000
			crossed = 0.000000
			total = 6521.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 4
		}
		records = {
			broker = {
				acronym = "BNYM"
				name = "BANK OF NEW YORK, THE"
				rank = 62
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 6271.000000
			crossed = 0.000000
			total = 6271.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 5
		}
		records = {
			broker = {
				acronym = "DBK"
				name = "DEUTSCHE BANK AG"
				rank = 63
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 5130.000000
			crossed = 0.000000
			total = 5130.000000
			highTouch = 0.000000
			lowTouch = 5130.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "DREX"
				name = "DREXEL HAMILTON LLC"
				rank = 64
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 3803.000000
			crossed = 0.000000
			total = 3803.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "JANY"
				name = "JANNEY MONTGOMERY SCOTT"
				rank = 65
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 3585.000000
			crossed = 0.000000
			total = 3585.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "MED"
				name = "MEDIOBANCA SPA"
				rank = 66
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 3049.000000
			crossed = 0.000000
			total = 3049.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 17
		}
		records = {
			broker = {
				acronym = "CLSA"
				name = "CLSA"
				rank = 67
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 3000.000000
			crossed = 0.000000
			total = 3000.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 2
		}
		records = {
			broker = {
				acronym = "LEER"
				name = "LEERINK SWANN & COMPANY"
				rank = 68
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 2120.000000
			crossed = 0.000000
			total = 2120.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "SCMC"
				name = "SCOTIA CAPITAL"
				rank = 69
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1906.000000
			crossed = 0.000000
			total = 1906.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "MIRA"
				name = "MIRABAUD SECURITIES"
				rank = 70
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1856.000000
			crossed = 0.000000
			total = 1856.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 2
		}
		records = {
			broker = {
				acronym = "RENC"
				name = "RENAISSANCE CAPITAL LIMITED"
				rank = 71
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1770.000000
			crossed = 0.000000
			total = 1770.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "EQUI"
				name = "EQUITA SIM SPA"
				rank = 72
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1678.000000
			crossed = 0.000000
			total = 1678.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 5
		}
		records = {
			broker = {
				acronym = "ENSK"
				name = "ENSKILDA SECURITIES"
				rank = 73
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1562.000000
			crossed = 0.000000
			total = 1562.000000
			highTouch = 1562.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "BCM"
				name = "BERENBERG CAPITAL MARKETS LLC"
				rank = 74
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1351.000000
			crossed = 0.000000
			total = 1351.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 14
		}
		records = {
			broker = {
				acronym = "BHL"
				name = "BANKHAUS LAMPE KG"
				rank = 75
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1205.000000
			crossed = 0.000000
			total = 1205.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "CBK"
				name = "COMMERZBANK"
				rank = 76
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 1084.000000
			crossed = 0.000000
			total = 1084.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 2
		}
		records = {
			broker = {
				acronym = "BABK"
				name = "BAADER BANK / HELVEA"
				rank = 77
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 956.000000
			crossed = 0.000000
			total = 956.000000
			highTouch = 606.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "MKMP"
				name = "MKM PARTNERS"
				rank = 78
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 500.000000
			crossed = 0.000000
			total = 500.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 1
		}
		records = {
			broker = {
				acronym = "CSMS"
				name = "CORNERSTONE MACRO LLC"
				rank = 79
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 408.000000
			crossed = 0.000000
			total = 408.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 6
		}
		records = {
			broker = {
				acronym = "RHC"
				name = "SUNTRUST CAPITAL MARKETS, INC."
				rank = 80
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 371.000000
			crossed = 0.000000
			total = 371.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
		}
		records = {
			broker = {
				acronym = "RMAC"
				name = "RENAISSANCE MACRO RESEARCH LL"
				rank = 81
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 95.000000
			crossed = 0.000000
			total = 95.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 2
		}
		records = {
			broker = {
				acronym = "SOVA"
				name = "SOVA CAPITAL LIMITED"
				rank = 82
			}
			topBrokers[] = {
			}
			bought = 0.000000
			sold = 0.000000
			traded = 32.000000
			crossed = 0.000000
			total = 32.000000
			highTouch = 0.000000
			lowTouch = 0.000000
			numReports = 3
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







