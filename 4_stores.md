# Group Stores
The Stores API provides basic store locator functionality.

## Find Stores [/stores/{storeSearchTerm}{?page,pageSize,searchLimit,storeType}]
### Search for a store [GET]
Search for a store based on the zip code, or city and state, entered by the user.
For example, a typical search by zip code can return all the stores available within 26 miles radius of that zip code.

+ Parameters
    + storeSearchTerm (required, string, `92108`) ... Zip code or StoreNumber or City/State to retrieve all the stores matching the criteria
    + page (optional, Integer, `1`) ... Used for pagination for search result. Default Value set to 1
    + pageSize (optional, string, `5`) ...Min 5 Max 10.  Used to indicate the number of results to be displayed in every call.Default Value set to 5
    + searchLimit (optional, string, `26`) ...  `searchLimit` refers to the radius and is used to fetch the store details with in the radius within which stores are availble. Allowed values - [between 26 and 50]. Default value is 26.
    + storeType (optional, string, `jcpStore`) ... storeType is used to tell the store type example values are 'jcpStore', 'jcpServices' and 'jcpOutlet'.

+ Request

            Example: http://api.jcpenney.com/v2/stores/75034?page=1&pageSize=5
            Example: http://api.jcpenney.com/v2/stores/plano,tx


+ Response 200

  + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, 'Stores`)

  + Body

            {
                "stores": [
                    {
                        "id":"1234",
                        "name": "King Of Prussia Plaz",
                        "number": "1234",
                        "street": "160 N Gulph Rd Ste 5000",
                        "city": "King Of Prussia",
                        "state": "PA",
                        "country": "USA",
                        "zip": "19406",
                        "phone": "(610)992-1096",
                        "distance": 1.1,
                        "latitude": 67,
                        "longitude": 99,
                        "services": [
                            "big and tall",
                            "custom decorating",
                            "furniture"
                        ],
                        "timings": [
                            {
                                "days": "Mon-Sat",
                                "time": "10:00am-9:00pm"
                            },
                            {
                                "days": "Sun",
                                "time": "11:00am-7:00pm"
                            }
                        ]
                    },
                    {
                        "id":"1234",
                        "name": "Montgomery Mall",
                        "number": "1234",
                        "street": "300 Montgomery Mall",
                        "city": "North Wales",
                        "state": "PA",
                        "country": "USA",
                        "zip": "19454",
                        "phone": "(215)362-2100",
                        "distance": 1.1,
                        "latitude": 67,
                        "longitude": 99,
                        "services": [
                            "big and tall",
                            "custom decorating",
                            "furniture"
                        ],
                        "timings": [
                            {
                                "days": "Mon-Sat",
                                "time": "10:00am-9:00pm"
                            },
                            {
                                "days": "Sun",
                                "time": "11:00am-7:00pm"
                            }
                        ]
                    }
                ],
                "pages": [
                    {
                        "url": "http://api.jcpenney.com/v2/stores/19406?page=1&searchLimit=10",
                        "number": 1,
                        "selected": true
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/stores/19406?page=2&searchLimit=10",
                        "number": 2,
                        "selected": false
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/stores/19406?page=3&searchLimit=10",
                        "number": 3,
                        "selected": false
                    }
                ]
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Stores result",
                "description": "Represents the response of store locator search results",
                "properties": {
                    "stores": {
                        "title": "list of stores",
                        "type": "array",
                        "items": {
                            "title": "Store",
                            "type": "object",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier for the JCPenney store."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "JCPenney store name."
                                },
                                "street": {
                                    "type": "string",
                                    "description": "Address line 1 or street address of the JCPenney store."
                                },
                                "city": {
                                    "type": "string",
                                    "description": "city where the JCPenney store is located."
                                },
                                "state": {
                                    "type": "string",
                                    "description": "state code/state abbreviation."
                                },
                                "zip": {
                                    "type": "string",
                                    "description": "zip code of the location where the JCPenney store is located."
                                },
                                "phone": {
                                    "type": "string",
                                    "description": "Formatted 10-digit phone number of the JCPenney store."
                                },
                                "distance": {
                                    "type": "double",
                                    "description": "distance of the store from the current location."
                                },
                                "timings": {
                                    "title": "List of timings",
                                    "type": "array",
                                    "items": {
                                        "title": "timing",
                                        "type": "object",
                                        "properties": {
                                            "days": {
                                                "type": "string",
                                                "description": "indicates the days when the store is open."
                                            },
                                            "time": {
                                                "type": "string",
                                                "description": "formatted time during which the store is open."
                                            },
                                            "note": {
                                                "type": "string",
                                                "description": "note assigned to the store."
                                            }
                                        },
                                        "required": [
                                            "days",
                                            "time"
                                        ]
                                    }
                                },
                                "services": {
                                    "title": "List of services provided by the store.",
                                    "type": "array",
                                    "items": {
                                        "title": "service",
                                        "type": "string",
                                        "description": "service provided by the JCPenney store."
                                    }
                                }
                            },
                            "required": [
                                "id",
                                "name",
                                "street",
                                "city",
                                "state",
                                "zip",
                                "phone",
                                "distance",
                                "timings",
                                "services"
                            ]
                        }
                    },
                    "pages": {
                        "title": "List of pages",
                        "type": "array",
                        "items": {
                            "title": "Store",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to the store details based on the page."
                                },
                                "number": {
                                    "type": "integer",
                                    "description": "Represents the page number.",
                                    "default": 1
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates whether the current page is selected.",
                                    "default": false
                                }
                            },
                            "required": [
                                "url",
                                "number",
                                "selected"
                            ]
                        }
                    }
                },
                "required": [
                    "stores",
                    "pages"
                ]
            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, Error`)

    + Body

            Response when the page number is invalid.
            {
                "errorCode": "SRV_PAGE_INVALID",
                "errorMessage": "The page number provided is invalid."
            }

            Response when page size is invalid.
            {
                "errorCode": "SRV_PAGESIZE_INVALID",
                "errorMessage": "The page size is not valid."
            }

            Response when search limit is invalid.
            {
                "errorCode": "SRV_SEARCHLIMIT_INVALID",
                "errorMessage": "The search limit is invalid."
            }

            Response when store type is invalid.
            {
                "errorCode": "SRV_STORETYPE_INVALID",
                "errorMessage": "The value of store type is invalid."
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Error",
                "description": "Represents the error in the system.",
                "properties": {
                    "errorCode": {
                    "type": "string",
                        "description": "Error code indicating the type of error."
                    },
                    "errorMessage": {
                        "type": "string",
                        "description": "Descriptive message for the error in the system."
                    }
                },
                "required": ["errorCode", "errorMessage"]
            }

+ Response 500

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "description": "Represents the error in the system.",
                "properties": {
                    "errorCode": {
                        "type": "string",
                        "description": "Error code indicating the type of error."
                    },
                    "errorMessage": {
                        "type": "string",
                        "description": "Descriptive message for the error in the system."
                    }
                },
                "required": [
                    "errorCode",
                    "errorMessage"
                ]
            }
