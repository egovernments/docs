---
description: Detailed steps to configure privacy in property tax module
---

# PT - Steps To Configure Privacy

## **Overview**

To ensure that the system works as expected after enabling privacy, we will require some configurations to be made in the environment. This document contains the steps to ensure the successful implementation and working of the Property Tax module.

## **Steps**

Following will be the changes required to move it to other environments:

* [x] Addition of index(for fuzzy search) in the property-service indexer file:\
  _Reference:_ [<img src="https://github.com/fluidicon.png" alt="" data-size="line">\[UM-5579\]- Added property fuzzy search topic and index in property-services by hinamakhija-eGov · Pull Request #2505 · egovernments/configs](https://github.com/egovernments/configs/pull/2505)\
  Also add a copy of the existing property-service index with a different topic name for the encryption process._Reference:_ [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/property-services.yml at ae525277c263a2d8ee516e5c4c83d53b40000bff · egovernments/configs](https://github.com/egovernments/configs/blob/ae525277c263a2d8ee516e5c4c83d53b40000bff/egov-indexer/property-services.yml#L956-L1053)
* [x] Restart the indexer
* [x] Add a new index in kibana with the name : pt-fuzzy-search-index and its mapping should be the same as the existing _**property-services**_ index.\
  **Index name:** `pt-fuzzy-search-index`
* [x] Copy the data from property-services index to this new index  pt-fuzzy-search-index.
* [x] Add a new persister file for the encryption process and verification.\
  File: [pt-enc-audit-persister.yml](https://github.com/egovernments/configs/blob/UAT/egov-persister/pt-enc-audit-persister.yml)
* [x] Update the path of the file in the DevOps repo in the specific environment file.
* [x] Restart the persister
* [x] Add the following json mappings in the existing mappings (parallel to property-services key) for property-services in Kibana so that the PII data is not visible during search(The data do remain in the index and also search with respect to this happens as is).

```
"_source": {
        "excludes": [
          "Data.street",
          "Data.doorNo",
          "Data.ownerNames"
        ]
      }
```

Sample index at the bottom.

* [x] Deploy new property-service build.
* [x] Port-forward the property-service pod and hit the curl to start encryption.\
  The curl can be referred from here:\
  **Property-encryption curl:**

```
curl --location --request POST 'http://localhost:8060/property-services/property/_encryptOldData?tenantIds=pb.amritsar&_=1657027355542&limit=200' \
--header 'authority: dev.digit.org' \
--header 'accept: application/json, text/plain, */*' \
--header 'accept-language: en-GB,en-US;q=0.9,en;q=0.8' \
--header 'content-type: application/json;charset=UTF-8' \
--header 'origin: https://dev.digit.org' \
--header 'referer: https://dev.digit.org/digit-ui/employee/pt/search' \
--header 'sec-ch-ua: ".Not/A)Brand";v="99", "Google Chrome";v="103", "Chromium";v="103"' \
--header 'sec-ch-ua-mobile: ?0' \
--header 'sec-ch-ua-platform: "Linux"' \
--header 'sec-fetch-dest: empty' \
--header 'sec-fetch-mode: cors' \
--header 'sec-fetch-site: same-origin' \
--header 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36' \
--data-raw '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "authToken": "14d2571d-33f0-47b3-a57f-866fb9b98989",
        "userInfo": {
            "id": 24226,
            "uuid": "11b0e02b-0145-4de2-bc42-c97b96264807",
            "userName": "amr001",
            "name": "leela",
            "mobileNumber": "9814424443",
            "emailId": "leela@llgmail.com",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "Grievance Routing Officer",
                    "code": "GRO",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC counter employee",
                    "code": "NOC_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PGR Last Mile Employee",
                    "code": "PGR_LME",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "BPA Field Inspector",
                    "code": "BPA_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL Field Inspector",
                    "code": "TL_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "pt emp",
                    "code": "PT_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Fire Noc Department Approver",
                    "code": "FIRE_NOC_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "BPA Services Approver",
                    "code": "BPA_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Counter Employee",
                    "code": "CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Counter Employee",
                    "code": "WS_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Field Inspector",
                    "code": "PT_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Field Inspector",
                    "code": "WS_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Property Tax Receipt Cancellator",
                    "code": "CR_PT",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "FSM Administrator",
                    "code": "FSM_ADMIN",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Document Inspector",
                    "code": "PT_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Employee",
                    "code": "EMPLOYEE",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL Counter Employee",
                    "code": "TL_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL Creator",
                    "code": "TL_CREATOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "BPAREG doc verifier",
                    "code": "BPAREG_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Universal Collection Employee",
                    "code": "UC_EMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "BPA Services verifier",
                    "code": "BPA_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC Field Inpector",
                    "code": "NOC_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Counter Approver",
                    "code": "PT_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Counter Employee",
                    "code": "SW_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Grievance Officer",
                    "code": "GO",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "FSM Employee Application Creator",
                    "code": "FSM_CREATOR_EMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Clerk",
                    "code": "SW_CLERK",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Property Approver",
                    "code": "Property Approver",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Clerk",
                    "code": "WS_CLERK",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC Doc Verifier",
                    "code": "NOC_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Birth and Death Dashboard User",
                    "code": "DASHBOARD_REPORT_VIEWER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "autoescalation emp",
                    "code": "AUTO_ESCALATE",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Document Verifier",
                    "code": "WS_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "FSM Employee Report Viewer",
                    "code": "FSM_REPORT_VIEWER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Document Verifier",
                    "code": "SW_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL Approver",
                    "code": "TL_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Field Employee",
                    "code": "FEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "FSM Payment Collector",
                    "code": "FSM_COLLECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "BPAREG Approver",
                    "code": "BPAREG_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "FSM Employee Application Editor",
                    "code": "FSM_EDITOR_EMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Collection Operator",
                    "code": "COLL_OPERATOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL doc verifier",
                    "code": "TL_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "FSM Employee Application Viewer",
                    "code": "FSM_VIEW_EMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "CSC Collection Operator",
                    "code": "CSC_COLL_OPERATOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "FSM Desluding Operator",
                    "code": "FSM_DSO",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Field Inspector",
                    "code": "SW_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Property Verifier",
                    "code": "Property Verifier",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "ptcollection emp",
                    "code": "PT_COLLECTION_EMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC counter Approver",
                    "code": "NOC_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Customer Support Representative",
                    "code": "CSR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "HRMS Admin",
                    "code": "HRMS_ADMIN",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "WS Approver",
                    "code": "WS_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Birth and Death User",
                    "code": "BND_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NOC Department Approver",
                    "code": "NOC_DEPT_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Super User",
                    "code": "SUPERUSER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "BPA NOC Verifier",
                    "code": "BPA_NOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "SW Approver",
                    "code": "SW_APPROVER",
                    "tenantId": "pb.amritsar"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": "Amritsar"
        },
        "plainAccessRequest": {
            
        },
        "msgId": "1657027355542|en_IN"
    }
}'
```

In the params list in both the above curls, “tenantIds” param can either be provided with a single tenantId or a list of tenantIds for encrypting the data with respect to the provided tenantIds. However, to encrypt the data for all tenantIds in the system, tenantIds param itself should be removed.

To validate if the encryption is completed, you can check with the following dB queries:

* `select * from eg_pt_enc_audit order by createdtime desc;`
* `select count(*) from eg_pt_id_enc_audit;`

With this query, it can be validated if all records are there or not. The count should match with the total count of records in the eg\_ws\_connection table.

* `select * from eg_pt_id_enc_audit;`

This can help you check what all properties have been updated so far. This table contains the id, applicationnumber, connectionnumber and tenantid.

&#x20;**Sample Index for point 8:**

```
PUT property-services
{
  "mappings": {
    "general": {
      "_source": {
        "excludes": [
          "Data.street",
          "Data.doorNo",
          "Data.ownerNames"
        ]
      },
      "properties": {
        "Data": {
          "properties": {
            "@timestamp": {
              "type": "date"
            },
            "accountId": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "acknowldgementNumber": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "auditDetails": {
              "properties": {
                "createdBy": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "createdTime": {
                  "type": "long"
                },
                "lastModifiedBy": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "lastModifiedTime": {
                  "type": "long"
                }
              }
            },
            "channel": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "creationReason": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "history": {
              "properties": {
                "action": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "assigner": {
                  "properties": {
                    "emailId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "id": {
                      "type": "long"
                    },
                    "mobileNumber": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "name": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "roles": {
                      "properties": {
                        "code": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "name": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "tenantId": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        }
                      }
                    },
                    "tenantId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "type": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "userName": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "uuid": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    }
                  }
                },
                "assignes": {
                  "properties": {
                    "emailId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "id": {
                      "type": "long"
                    },
                    "mobileNumber": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "name": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "roles": {
                      "properties": {
                        "code": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "name": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "tenantId": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        }
                      }
                    },
                    "tenantId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "type": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "userName": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "uuid": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    }
                  }
                },
                "auditDetails": {
                  "properties": {
                    "createdBy": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "createdTime": {
                      "type": "long"
                    },
                    "lastModifiedBy": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "lastModifiedTime": {
                      "type": "long"
                    }
                  }
                },
                "businessId": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "businessService": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "businesssServiceSla": {
                  "type": "long"
                },
                "comment": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "documents": {
                  "properties": {
                    "auditDetails": {
                      "properties": {
                        "createdBy": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "createdTime": {
                          "type": "long"
                        },
                        "lastModifiedBy": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "lastModifiedTime": {
                          "type": "long"
                        }
                      }
                    },
                    "documentType": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "fileStoreId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "id": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "tenantId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    }
                  }
                },
                "id": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "moduleName": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "nextActions": {
                  "properties": {
                    "action": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "currentState": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "nextState": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "roles": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "tenantId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "uuid": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    }
                  }
                },
                "previousStatus": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "rating": {
                  "type": "long"
                },
                "state": {
                  "properties": {
                    "actions": {
                      "properties": {
                        "action": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "currentState": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "nextState": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "roles": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "tenantId": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        },
                        "uuid": {
                          "type": "text",
                          "fields": {
                            "keyword": {
                              "type": "keyword",
                              "ignore_above": 256
                            }
                          }
                        }
                      }
                    },
                    "applicationStatus": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "businessServiceId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "docUploadRequired": {
                      "type": "boolean"
                    },
                    "isStartState": {
                      "type": "boolean"
                    },
                    "isTerminateState": {
                      "type": "boolean"
                    },
                    "sla": {
                      "type": "long"
                    },
                    "state": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "tenantId": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "uuid": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    }
                  }
                },
                "stateSla": {
                  "type": "long"
                },
                "tenantId": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                }
              }
            },
            "id": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "landArea": {
              "type": "long"
            },
            "noOfFloors": {
              "type": "long"
            },
            "oldPropertyId": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "owners": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "ownershipCategory": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "propertyId": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "propertyType": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "source": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "status": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "superBuiltUpArea": {
              "type": "float"
            },
            "surveyId": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "tenantData": {
              "properties": {
                "OfficeTimings": {
                  "properties": {
                    "Mon - Fri": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "Sat": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    }
                  }
                },
                "address": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "city": {
                  "properties": {
                    "code": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "ddrName": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "latitude": {
                      "type": "float"
                    },
                    "longitude": {
                      "type": "float"
                    },
                    "name": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "ulbGrade": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    }
                  }
                },
                "code": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "contactNumber": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "description": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "domainUrl": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "emailId": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "facebookUrl": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "helpLineNumber": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "imageId": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "logoId": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "name": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "pdfContactDetails": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },	
                "pdfHeader": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "pincode": {
                  "type": "long"
                },
                "twitterUrl": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "type": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                }
              }
            },
            "tenantId": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "units": {
              "properties": {
                "active": {
                  "type": "boolean"
                },
                "arv": {
                  "type": "long"
                },
                "constructionDetail": {
                  "properties": {
                    "builtUpArea": {
                      "type": "float"
                    },
                    "carpetArea": {
                      "type": "long"
                    },
                    "constructionDate": {
                      "type": "long"
                    },
                    "constructionType": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "plinthArea": {
                      "type": "long"
                    },
                    "superBuiltUpArea": {
                      "type": "long"
                    }
                  }
                },
                "floorNo": {
                  "type": "long"
                },
                "id": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "occupancyDate": {
                  "type": "long"
                },
                "occupancyType": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "tenantId": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "unitType": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "usageCategory": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                }
              }
            },
            "usageCategory": {
              "type": "text",
              "fields": {
                "keyword": {
                  "type": "keyword",
                  "ignore_above": 256
                }
              }
            },
            "ward": {
              "properties": {
                "boundaryNum": {
                  "type": "long"
                },
                "children": {
                  "properties": {
                    "area": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "boundaryNum": {
                      "type": "long"
                    },
                    "code": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "label": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "latitude": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "longitude": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "name": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "pincode": {
                      "type": "long"
                    }
                  }
                },
                "code": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "label": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                },
                "name": {
                  "type": "text",
                  "fields": {
                    "keyword": {
                      "type": "keyword",
                      "ignore_above": 256
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```



