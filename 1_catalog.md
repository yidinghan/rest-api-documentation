# Group Catalog
This document explains the functionalities exposed by Catalog REST API. Catalog consists of departments, categories and products. At the top level of the hierarchy is a department. Each department contains sub categories underneath it, and each category can contain either sub categories or products. Consumers can either browse through the catalog or search the catalog.
Consumers can view detailed information about the product along with inventory and price information for a specific store or online channel. The API also provides list of recommended products for a given product and ability for user to view and add reviews to a given product.

## Departments [/departments]
Departments are the root elements in the catalog. Categories are assigned to a department and can be used to form the catalog navigational hierarchy.

### Department list [GET]
Retrieves all active/available departments in the catalog.

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Department[]')

    + Body

            [
                {
                    "id": "dept20000011",
                    "url": "http://api.jcpenney.com/v2/departments/dept20000011",
                    "name": "for the home",
                    "clearance": false
                },
                {
                    "id": "dept20000012",
                    "url": "http://api.jcpenney.com/v2/departments/dept20000012",
                    "name": "bed & bath",
                    "clearance": false
                },
                {
                    "id": "dept20022800026",
                    "url": "http://api.jcpenney.com/v2/departments/dept20022800026",
                    "name": "window",
                    "clearance": false
                },
                {
                    "id": "dept20000013",
                    "url": "http://api.jcpenney.com/v2/departments/dept20000013",
                    "name": "women",
                    "clearance": false
                },
                {
                    "id": "dept20000014",
                    "url": "http://api.jcpenney.com/v2/departments/dept20000014",
                    "name": "men",
                    "clearance": false
                },
                {
                    "id": "dept20021210041",
                    "url": "http://api.jcpenney.com/v2/departments/dept20021210041",
                    "name": "clearance",
                    "clearance": true
                }
            ]

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of departments",
                "type": "array",
                "items": {
                    "title": "Department",
                    "type": "object",
                    "properties": {
                        "id": {
                            "type": "string",
                            "description": "Unique identifier for the department."
                        },
                        "url": {
                            "type": "URL",
                            "description": "URL to retrieve the department information."
                        },
                        "name": {
                            "type": "string",
                            "description": "Name of the department."
                        },
                        "clearance": {
                            "type": "boolean",
                            "description": "Indicates whether the department is a clearance department",
                            "default": false
                        },
                        "image": {
                            "type": "URL",
                            "description": "URL to the image assigned to the department."
                        },
                        "highResolutionImage": {
                            "type": "URL",
                            "description": "URL to the highResolutionImage assigned to the department."
                        }
                    },
                    "required": [
                        "id",
                        "url",
                        "name",
                        "clearance"
                    ]
                }
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



## Department [/departments/{departmentId}]
The department resource provides complete information about the department and also provides information about the categories assigned to the department.
An active department has at least one category assigned to it.

### Get a department [GET]
Retrieves a single department resource matching the department id passed in the request URL.

+ Parameters
    + departmentId (required, String, `dept20000013`) ... Unique identifier for the department.

+ Response 200


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Department')

    + Body

            {
                "id": "dept20000013",
                "name": "women",
                "clearance": false,
                "categories": [
                    {
                        "id": "cat20000013",
                        "url": "http://api.jcpenney.com/v2/categories/cat20000013",
                        "name": "SHOP SPECIAL SIZES",
                        "clearance": false,
                        "brand": false,
                        "header": true
                    },
                    {
                        "id": "cat2000014",
                        "url": "http://api.jcpenney.com/v2/categories/cat2000014",
                        "name": "SHOP CLOTHING",
                        "clearance": false,
                        "brand": false,
                        "header": true
                    },
                    {
                        "id": "cat2000015",
                        "url": "http://api.jcpenney.com/v2/categories/cat2000015",
                        "name": "SHOP ACCESSORIES",
                        "clearance": false,
                        "brand": false,
                        "header": true
                    },
                    {
                        "id": "cat2000016",
                        "url": "http://api.jcpenney.com/v2/categories/cat2000016",
                        "name": "SHOP BRANDS",
                        "clearance": false,
                        "brand": false,
                        "header": true
                    },
                    {
                        "id": "cat2000017",
                        "url": "http://api.jcpenney.com/v2/categories/cat2000017",
                        "name": "EXPLORE SHOPS",
                        "clearance": false,
                        "brand": false,
                        "header": true
                    },
                    {
                        "id": "cat2000018",
                        "url": "http://api.jcpenney.com/v2/categories/cat2000018",
                        "name": "SHOP SALE & CLEARANCE",
                        "clearance": false,
                        "brand": false,
                        "header": true
                    }
                ]
            }

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "type": "object",
                "title": "Department",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier of the department."
                    },
                    "name": {
                        "type": "string",
                        "description": "Name of the department."
                    },
                    "clearance": {
                        "type": "boolean",
                        "description": "Indicates whether the department is a clearance department.",
                        "default": false
                    },
                    "image": {
                        "type": "URL",
                        "description": "URL to the image assigned to the department."
                    },
                    "highResolutionImage": {
                        "type": "URL",
                        "description": "URL to the highResolutionImage assigned to the department."
                    },
                    "categories": {
                        "type": "array",
                        "title": "Categories set",
                        "items": {
                            "type": "object",
                            "title": "Category",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier of the category."
                                },
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the sub-categories assigned to the category."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the category."
                                },
                                "clearance": {
                                    "type": "boolean",
                                    "description": "Indicates whether the category is a clearance category.",
                                    "default": false
                                },
                                "brand": {
                                    "type": "boolean",
                                    "description": "Indicates whether the category is a brand category.",
                                    "default": false
                                },
                                "header": {
                                    "type": "boolean",
                                    "description": "Indicates whether the category is a Header category.",
                                    "default": false
                                },
                                "image": {
                                    "type": "URL",
                                    "description": "URL to the image assigned to the category."
                                },
                                "highResolutionImage": {
                                    "type": "URL",
                                    "description": "URL to the highResolutionImage assigned to the category."
                                }
                            },
                            "required": [
                                "id",
                                "url",
                                "name",
                                "clearance",
                                "brand",
                                "Header"
                            ]
                        }
                    }
                },
                "required": [
                    "id",
                    "name",
                    "clearance"
                ]
            }



+ Response 404


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_DEPARTMENT_NOTFOUND",
                "errorMessage": "Department not found."
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

+ Response 500


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errrorCode": "SRV_GENERIC_ERROR",
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


## Category [/categories/{categoryId}]
A category represents a navigational node in the catalog hierarchy. A category can contain categories or products.

There are three types of categories clearance categories, header categories and brand categories. The type of category is represented by the corresponding boolean field.
It is possible for a category to belong to more than one category type.

### Get a category [GET]
Retrieve category resource matching the category id passed in the requested URL.

+ Parameters

    + categoryId (required, String, `cat100240031`) ... Unique identifier of category.

+ Response 200


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Category')

    + Body

            {
                "id": "cat20000013",
                "name": "SHOP SPECIAL SIZES",
                "clearance": false,
                "brand": false,
                "header": true,
                "categories": [
                    {
                        "id": "cat100240005",
                        "url": "http://api.jcpenney.com/v2/categories/cat100240005",
                        "name": "plus size",
                        "clearance": false,
                        "brand": false,
                        "header": false
                    },
                    {
                        "id": "cat100250027",
                        "url": "http://api.jcpenney.com/v2/categories/cat100250027",
                        "name": "petites",
                        "clearance": false,
                        "brand": false,
                        "header": false
                    },
                    {
                        "id": "cat100250030",
                        "url": "http://api.jcpenney.com/v2/categories/cat100250030",
                        "name": "talls",
                        "clearance": false,
                        "brand": false,
                        "header": false
                    },
                    {
                        "id": "cat100250032",
                        "url": "http://api.jcpenney.com/v2/categories/cat100250032",
                        "name": "maternity",
                        "clearance": false,
                        "brand": false,
                        "header": false
                    }
                ]
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Categories",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier of the category."
                    },
                    "name": {
                        "type": "string",
                        "description": "Name of the category."
                    },
                    "clearance": {
                        "type": "boolean",
                        "description": "Indicates whether the category is a clearance category.",
                        "default": false
                    },
                    "brand": {
                        "type": "boolean",
                        "description": "Indicates whether the category represents a brand.",
                        "default": false
                    },
                    "header": {
                        "type": "boolean",
                        "description": "Indicates whether the category is a header category.",
                        "default": false
                    },
                    "image": {
                        "type": "URL",
                        "description": "URL to the image assigned to the category."
                    },
                    "highResolutionImage": {
                        "type": "URL",
                        "description": "URL to the high resolution image associated to the category."
                    },
                    "categories": {
                        "type": "array",
                        "title": "Set of categories",
                        "items": {
                            "type": "object",
                            "title": "Category",
                             "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier of the category."
                                },
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the sub-categories or products assigned to the category."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the category."
                                },
                                "clearance": {
                                    "type": "boolean",
                                    "description": "Indicates whether the category is a clearance category.",
                                    "default": false
                                },
                                "brand": {
                                    "type": "boolean",
                                    "description": "Indicates whether the category is a brand category.",
                                    "default": false
                                },
                                "header": {
                                    "type": "boolean",
                                    "description": "Indicates whether the ctaegory is a header category.",
                                    "default": false
                                },
                                "image": {
                                    "type": "boolean",
                                    "description": "URL to the image assigned to the category."
                                },
                                "highResolutionImage": {
                                    "type": "URL",
                                    "description": "URL to the high resolution image associated to the category."
                                }
                            },
                            "required": [
                                "id",
                                "url",
                                "name",
                                "clearance",
                                "brand",
                                "header"
                            ]
                        }
                    }
                },
                "required": [
                    "id",
                    "name",
                    "clearance",
                    "brand",
                    "header"
                ]
            }

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_CATEGORY_NOTFOUND",
                "errorMessage": "Category not found."
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



## Products [/categories/{categoryId}/products{?filters,page,pageSize,sortBy}]
A category can contain one or more products. It returns a list of products that belongs to the given category along with facet information, sort options and pagination.

Note: Prices provided in the response always represent Online price for the product.

### Get products in a category. [GET]
Retrieves the products in a category.

+ Parameters

    + categoryId (required, String, `cat100240031`) ... Unique identifier of category.
    + page (optional, Integer, `2`) ... Used for pagination of products.
    + pageSize (optional, Integer, `24`) ... Min 24 Max 96. default: 24. Used to indicate the number of products to be retrieved. If the number of products requested is more than the number of products assigned to the category then all the products in the category are returned.
    + sortBy (optional, String, `pricehightolow`) ... one of ('featured', 'pricehightolow', 'pricelowtohigh', 'ratingshightolow', 'ratingslowtohigh'). default: 'featured'. Used for sorting the products.
    + filters (optional, String, `1234`) ... Used for facet navigation of products.

+ Request

            Example: http://api.jcpenney.com/v2/categories/cat100240031/products?filters=600000&page=2&pageSize=24&sortBy=featured

    + Headers

            X-Currency: String ... (optional, String, `USD`)


+ Response 200


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Products')

    + Body

            {
                "id": "cat100210008",
                "name": "dresses",
                "clearance": false,
                "brand": false,
                "header": false,
                "products": [
                    {
                        "id": "pp5003200163",
                        "url": "http://api.jcpenney.com/v2/products/pp5003200163",
                        "name": "9 & Co.® Ruffle-Front Dress",
                        "isNew": false,
                        "rating": 0,
                        "reviewCount": 0,
                        "images": [
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP0905201317011659M.tif",
                                "swatchUrl": "http://zoom.jcpenney.com/is/image/DP0905201317011659M.tif",
                                "type": "PRIMARY",
                                "altText": "9 & Co.® Ruffle-Front Dress"
                            }
                        ],
                        "prices": [
                            {
                                "type": "ORIGINAL",
                                "min": 70,
                                "max": 70
                            },
                            {
                                "type": "SALE",
                                "min": 27.99,
                                "max": 27.99
                            }
                        ]
                    },
                    {
                        "id": "pp5003230750",
                        "url": "http://api.jcpenney.com/v2/products/pp5003230750",
                        "name": "Studio 1® Sweater Dress",
                        "isNew": false,
                        "rating": 4.7,
                        "reviewCount": 3,
                        "images": [
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP1030201318275736C.tif",
                                "swatchUrl": "http://www.jcpenney.com/dotcom/images/DP0925201317032943S.jpg",
                                "type": "PRIMARY",
                                "altText": "Black/Ivory"
                            },
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP0925201317032993M.tif",
                                "swatchUrl": "http://www.jcpenney.com/dotcom/images/DP0925201317032694S.jpg",
                                "type": "SWATCH",
                                "altText": "Black/grey/Ivory"
                            },
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP0925201317032993M.tif",
                                "swatchUrl": "http://www.jcpenney.com/dotcom/images/DP0925201317032444S.jpg",
                                "type": "SWATCH",
                                "altText": "Drk Grey/grey/ivor"
                            }
                        ],
                        "prices": [
                            {
                                "type": "ORIGINAL",
                                "min": 50,
                                "max": 50
                            },
                            {
                                "type": "SALE",
                                "min": 19.99,
                                "max": 19.99
                            }
                        ]
                    },
                    {
                        "id": "pp5003460186",
                        "url": "http://api.jcpenney.com/v2/products/pp5003460186",
                        "name": "R&K Originals® Belted V-Neck Sweater Dress",
                        "isNew": true,
                        "rating": 0,
                        "reviewCount": 0,
                        "images": [
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP1018201317020918M.tif",
                                "swatchUrl": "http://www.jcpenney.com/dotcom/images/DP1021201317025786S.jpg",
                                "type": "PRIMARY",
                                "altText": "Cherry"
                            },
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP1018201317020918M.tif",
                                "swatchUrl": "http://www.jcpenney.com/dotcom/images/DP1021201317030536S.jpg",
                                "type": "SWATCH",
                                "altText": "Grey"
                            }
                        ],
                        "prices": [
                            {
                                "type": "ORIGINAL",
                                "min": 60,
                                "max": 60
                            },
                            {
                                "type": "SALE",
                                "min": 29.99,
                                "max": 29.99
                            }
                        ]
                    }
                ],
                "filters": [
                    {
                        "id": "600000",
                        "name": "CATEGORIES",
                        "type": "DEFAULT",
                        "values": [
                            {
                                "id": "100250202",
                                "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?sortBy=featured&page=1&pageSize=24&filters=100250202",
                                "name": "$40 & under",
                                "count": 321,
                                "selected": false,
                                "available": true
                            },
                            {
                                "id": "100250208",
                                "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?sortBy=featured&page=1&pageSize=24&filters=100250208",
                                "name": "bridal dresses",
                                "count": 30,
                                "selected": false,
                                "available": true
                            }
                        ]
                    },
                    {
                        "id": "29",
                        "name": "SIZE RANGE",
                        "type": "DEFAULT",
                        "values": [
                            {
                                "id": "1724",
                                "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?sortBy=featured&page=1&pageSize=24&filters=1724",
                                "name": "juniors",
                                "count": 288,
                                "selected": false,
                                "available": true
                            }
                        ]
                    }
                ],
                "pages": [
                    {
                        "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?pageNum=1&pageSize=24",
                        "number": 1,
                        "selected": true
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?pageNum=2&pageSize=24",
                        "number": 2,
                        "selected": false
                    }
                ],
                "sortOptions": [
                    {
                        "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?pageNum=1&pageSize=24&sortBy=featured",
                        "name": "featured",
                        "selected": true,
                        "order": 1
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?pageNum=1&pageSize=24&sortBy=pricehightolow",
                        "name": "price high - low",
                        "selected": false,
                        "order": 2
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?pageNum=1&pageSize=24&sortBy=pricelowtohigh",
                        "name": "price low - high",
                        "selected": false,
                        "order": 3
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/categories/cat100210008/products?pageNum=1&pageSize=24&sortBy=ratingshightolow",
                        "name": "ratings high - low",
                        "selected": false,
                        "order": 4
                    }
                ]
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Products",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier of the category."
                    },
                    "name": {
                        "type": "string",
                        "description": "Name of the category."
                    },
                    "clearance": {
                        "type": "boolean",
                        "description": "Indicates whether the category is a clearance category.",
                        "default": false
                    },
                    "brand": {
                        "type": "boolean",
                        "description": "Indicates whether the category is a brand.",
                        "default": false
                    },
                    "header": {
                        "type": "boolean",
                        "description": "Indicates whether the category is a Header category.",
                        "default": false
                    },
                    "image": {
                        "type": "URL",
                        "description": "URL to the image assigned to the category."
                    },
                    "highResolutionImage": {
                        "type": "URL",
                        "description": "URL to the highResolutionImage assigned to the category."
                    },
                    "count": {
                        "type": "long",
                        "description": "Number of products in the category."
                    },
                    "products": {
                        "title": "List of products",
                        "type": "array",
                        "description": "Array of products",
                        "items": {
                            "title": "Product",
                            "type": "object",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier of the product."
                                },
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the product detail information."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the product."
                                },
                                "isNew": {
                                    "type": "boolean",
                                    "description": "Indicates that the product is a new product.",
                                    "default": false
                                },
                                "rating": {
                                    "type": "double",
                                    "description": "Average rating of the product.",
                                    "default": 0
                                },
                                "reviewCount": {
                                    "type": "integer",
                                    "description": "Number of reviews for the product",
                                    "default": 0
                                },
                                "images": {
                                    "title": "List of images for the product",
                                    "type": "array",
                                    "items": {
                                        "title": "Image",
                                        "type": "object",
                                        "properties": {
                                            "url": {
                                                "type": "URL",
                                                "description": "URL to the product image."
                                            },
                                            "swatchUrl": {
                                                "type": "URL",
                                                "description": "URL to the swatch image for the product."
                                            },
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "PRIMARY",
                                                    "ALTERNATE",
                                                    "SWATCH"
                                                ],
                                                "description": "Indicates the type of product image."
                                            },
                                            "altText": {
                                                "type": "string",
                                                "description": "Alternate text for the image."
                                            }
                                        },
                                        "required": [
                                            "url",
                                            "type"
                                        ]
                                    }
                                },
                                "prices": {
                                    "title": "Array of prices for the product.",
                                    "type": "array",
                                    "items": {
                                        "title": "Price",
                                        "type": "object",
                                        "properties": {
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "ORIGINAL",
                                                    "SALE",
                                                    "CLEARANCE",
                                                    "MSRP"
                                                ],
                                                "description": "Indicates the type of price."
                                            },
                                            "min": {
                                                "type": "double",
                                                "description": "minimum price amount for the product.",
                                                "default": 0
                                            },
                                            "max": {
                                                "type": "double",
                                                "description": "maximum price amount for the product.",
                                                "default": 0
                                            }
                                        },
                                        "required": [
                                            "type",
                                            "min",
                                            "max"
                                        ]
                                    }
                                },
                                "messages": {
                                    "title": "List of messages for the product",
                                    "type": "array",
                                    "items": {
                                        "title": "Message",
                                        "type": "object",
                                        "properties": {
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "CHANNEL_MESSAGING",
                                                    "PROMOTION",
                                                    "TRUCK_DELIVERY"
                                                ],
                                                "description": "Indicates the type of message."
                                            },
                                            "title": {
                                                "type": "string",
                                                "description": "Title of the message"
                                            },
                                            "text": {
                                                "type": "string",
                                                "description": "Detail description of the message."
                                            }
                                        },
                                        "required": [
                                            "type",
                                            "title",
                                            "text"
                                        ]
                                    }
                                }
                            },
                            "required": [
                                "id",
                                "url",
                                "name",
                                "isNew",
                                "rating",
                                "reviewCount",
                                "prices"
                            ]
                        }
                    },
                    "filters": {
                        "title": "Set of filters for facet navigation of products",
                        "type": "array",
                        "items": {
                            "title": "Filter",
                            "type": "object",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "unique identifier for the filter."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "name of the filter."
                                },
                                "type": {
                                    "type": "string",
                                    "enum": [
                                        "DEFAULT",
                                        "RANGE",
                                        "PRICE_RANGE"
                                    ],
                                    "description": "Indicates the type of filter."
                                },
                                "values": {
                                    "title": "List of filter values which can be applied.",
                                    "type": "array",
                                    "items": {
                                        "title": "FilterValue",
                                        "type": "object",
                                        "properties": {
                                            "id": {
                                                "type": "string",
                                                "description": "Unique identifier for the filter value."
                                            },
                                            "url": {
                                                "type": "URL",
                                                "description": "URL to be used to apply the filter."
                                            },
                                            "name": {
                                                "type": "string",
                                                "description": "name of the filter value"
                                            },
                                            "image": {
                                                "type": "URL",
                                                "description": "URL to the image assigned to the dimension value."
                                            },
                                            "count": {
                                                "type": "integer",
                                                "description": "Count of products for which the filter value is applicable.",
                                                "default": 0
                                            },
                                            "selected": {
                                                "type": "boolean",
                                                "description": "Indicates whether the current filter value is selected for the product.",
                                                "default": false
                                            },
                                            "available": {
                                                "type": "boolean",
                                                "description": "Indicates whether the current filter value is available for selection.",
                                                "default": true
                                            }
                                        },
                                        "required": [
                                            "id",
                                            "url",
                                            "name",
                                            "image",
                                            "count",
                                            "selected",
                                            "available"
                                        ]
                                    }
                                }
                            },
                            "required": [
                                "id",
                                "name",
                                "type",
                                "values"
                            ]
                        }
                    },
                    "pages": {
                        "title": "Set of pages for supporting pagination",
                        "type": "object",
                        "items": {
                            "title": "page",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to be used to retrieve the products in the required page."
                                },
                                "number": {
                                    "type": "integer",
                                    "description": "Page number",
                                    "default": 1
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates if the current page object is selected.",
                                    "default": false
                                }
                            },
                            "required": [
                                "url",
                                "number",
                                "selected"
                            ]
                        }
                    },
                    "sortOptions": {
                        "title": "List of sort options applicable to the products.",
                        "type": "array",
                        "items": {
                            "title": "SortOption",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to be used to retrieve the products sorted in a particular order."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the sort option."
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates if the sort option is selected.",
                                    "default": false
                                },
                                "order": {
                                    "type": "integer",
                                    "description": "order of the sort option to be displayed.",
                                    "default": 1
                                }
                            },
                            "required": [
                                "url",
                                "name",
                                "selected",
                                "order"
                            ]
                        }
                    }
                },
                "required": [
                    "id",
                    "name",
                    "clearance",
                    "brand",
                    "Header"
                ]
            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            Request contains an invalid page.

            {
                "errorCode": "SRV_PAGE_INVALID",
                "errorMessage": "Page number provided is not applicable to the current request."
            }

            Request contains invalid page size.

            {
                "errorCode": "SRV_PAGESIZE_INVALID",
                "Page size provided is invalid. Only value between 24 and 96 is allowed."
            }

            Request contains invalid sort option.

            {
                "errorCode": "SRV_SORTBY_INVALID",
                "errorMessage": "Sort by value provided is invalid. SortBy value should be one of: [featured, pricehightolow, pricelowtohigh, ratingshightolow]."
            }

            Request contains an invalid filter value.

            {
                "errorCode": "SRV_FILTER_INVALID",
                "errorMessage": "The filter value provided is not applicable to the current request."
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

+ Response 404


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_CATEGORY_NOTFOUND",
                "errorMessage": "Category not found."
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


## Product [/products/{productId}{?page,pageSize,storeNumber,storeAddress}]

Catalog contains different types of products such as:

- Regular products : Products with LOT/SKU/COLOR Options
- Single lot, single sku : Product with no LOT/SKU/COLOR options
- Ensemble : Product containing group of Products
- Products with Service agreements and warranties : Product contains service agreements and warranties. When such a product is added the product and the service agreement can be added to the cart/favorites.
- Products with variable data : Products such as monogram products, hemming products, gift cards, made to measure products.

### Get a product [GET]

Retrieves the product resource matching the product id passed in the requested URL.


+ Parameters

    + productId (required, String, `pp5002310768`) ... Unique identifier of the Product for which details are required.
    + page (optional, string, `1`) ... Page Number for which the store information is to be retrieved.
    + pageSize (optional, string, `24`) ... Min 24 Max 96. default: 24. Number of store results to be retrieved.
    + storeNumber (optional, string, `2795`) ... JCPenney store number for which pricing and inventory of nearby stores is to be retrieved.
    + storeAddress (optional, string, `19406/plano,texas/32.767,-117.17`) ... zip code/city state/longitude latitude for which pricing and inventory in near by JCPenney stores is to be retrieved.

+ Request


    + Headers

            X-Currency: String ... (optional, String, `USD`)

+ Response 200


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Product')

    + Body

            The examples below are cases when the sku selection has been completed.
            Some of the parameters such as skuId are not provided when sku selection is inprogress.

            **Response for a regular product**.

            {
                "id": "pp5002770550",
                "name": "Grecian Wrap Dress",
                "isNew": false,
                "rating": 0,
                "reviewCount": "0",
                "type": "REGULAR",
                "description": "<p>Wrap yourself in the Grecian-inspired draping of our fabulously flattering dress.</p>\r\n",
                "recommedationsUrl": "http://api.jcpenney.com/v2/products/pp5002770550/recommendations",
                "skuId": "22906380042",
                "inventory": {
                    "status": "AVAILABLE_LOW",
                    "message": "limited stock available"
                },
                "images": [
                    {
                        "url": "http://zoom.jcpenney.com/is/image/DP0424201317003965M.tif",
                        "type": "PRIMARY",
                        "altText": "Grecian Wrap Dress"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/DP0424201317003965M.tif",
                        "type": "ALTERNATE",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/DP0424201317003965M.tif",
                        "altText": "Grecian Wrap Dress"
                    }
                ],
                "prices": [
                    {
                        "max": 80,
                        "min": 80,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 39.99,
                        "min": 39.99,
                        "type": "CLEARANCE"
                    }
                ],
                "options": [
                    {
                        "name": "SIZE",
                        "type": "SKU_OPTION",
                        "optionValues": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=4",
                                "selected": false,
                                "available": false,
                                "value": "4"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=6",
                                "selected": false,
                                "available": false,
                                "value": 6
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=8",
                                "selected": true,
                                "available": true,
                                "value": 8
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=10",
                                "selected": false,
                                "available": false,
                                "value": 10
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=12",
                                "selected": false,
                                "available": false,
                                "value": 12
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=14",
                                "selected": false,
                                "available": false,
                                "value": 14
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=16",
                                "selected": false,
                                "available": false,
                                "value": 16
                            }
                        ]
                    },
                    {
                        "name": "COLOR",
                        "type": "COLOR_OPTION",
                        "optionValues": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002770550?SIZE=8&COLOR=Soc.cerise",
                                "selected": true,
                                "available": true,
                                "value": "Soc.cerise",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/DP0424201317003987S.jpg",
                                    "type": "SWATCH",
                                    "altText": "Soc.cerise"
                                }
                            }
                        ]
                    }
                ]
            }

            **Response for a product with service agreement**.
            Note: The response also holds good for a single lot single sku product.

            {
                "id": "1845342",
                "name": "Hoover® Carpet Cleaning Steam Vacuum",
                "isNew": false,
                "rating": 3.86,
                "reviewCount": 7,
                "reviewsURL": "http://api.jcpenney.com/v2/products/1845342/reviews",
                "type": "REGULAR",
                "description": "<p>\r\n\tSteamVac TurboPower carpet cleaner with SpinScrub gives your carpets and floors professional-looking results whenever you want without having to rent.</p>\r\n",
                "recommendationsURL": "http://api.jcpenney.com/v2/products/1845342/recommendations",
                "skuId": "86930540018",
                "inventory": {
                    "status": "AVAILABLE",
                    "message": "Available"
                },
                "images": [
                    {
                        "url": "http://zoom.jcpenney.com/is/image/0900631b818648d3M.tif",
                        "type": "PRIMARY",
                        "altText": "Hoover%C2%AE+Carpet+Cleaning+Steam+Vacuum"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/0900631b818648d3M.tif",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/0900631b818648d3M.tif",
                        "type": "ALTERNATE",
                        "altText": "Hoover%C2%AE+Carpet+Cleaning+Steam+Vacuum"
                    }
                ],
                "prices": [
                    {
                        "max": 120,
                        "min": 120,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 120,
                        "min": 120,
                        "type": "DEFAULT"
                    }
                ],
                "serviceAgreements": [
                    {
                        "name": "1YR SVS PLAN POS",
                        "data": "Your new floor care appliance is a real labor saver.  It works hard so you don�t have to!  Relax, it's easy to keep it working hard for you.  Just add a Purchase Protection Plan.The original product warranty covers parts and labor for 24 months (2 Years) from the date of purchase.Your new floor care appliance works hard so you don�t have to! Keep it running smoothly with a Purchase Protection Plan! Protect yourself against unexpected failures and expensive repairs.  The Purchase Protection Plan takes over when the manufacturer�s warranty ends providing 12 months of additional coverage.  If anything goes wrong with your new floor care product during the term of coverage, we�ll replace it. Simple as that! No hassles! No additional charges! No kidding!",
                        "selected": false,
                        "itemId": "86991460000",
                        "url": "http://api.jcpenney.com/v2/products/1845342?COLOR=Black&SERVICE_AGREEMENT=true",
                        "prices": [
                            {
                                "max": 11,
                                "min": 11,
                                "type": "ORIGINAL"
                            },
                            {
                                "max": 11,
                                "min": 11,
                                "type": "DEFAULT"
                            }
                        ]
                    }
                ],
                "warranties": [
                    {
                        "title": "REPAIR: CARRY-IN                        LABOR: 2 Y",
                        "description": "N5998                                                            N5998Sub 869                                                               Jun 2006                                                                                      Full Two Year Warranty                                                    (Domestic use)                                                                                                  Your HOOVER® appliance is warranted in normal household use, in       accordance with the Owner's Manual against original defects in        material and workmanship for a period of two full years from          date of purchase. This warranty provides, at no cost to you, all      labor and parts to place this appliance in correct operating          condition during the warranted period. This warranty applies          when the appliance is purchased in the United States including        its territories and possessions, or in Canada or from a U. S.         Military Exchange. Appliances purchased elsewhere are covered by      a limited one year warranty which covers the cost of parts only.      This warranty does not apply if the appliance is used in a            commercial or rental application.                                     \n                                                                      This warranty only applies when the product is in use in the          country or territory in which it is purchased.                                                                                              Warranty service can only be obtained by presenting the               appliance to one of the following authorized warranty service         outlets. Proof of purchase will be required before service is         rendered.                                                                                                                                   1. Hoover Sales and Service Centers                                                                                                         2. Hoover Authorized Warranty Service Dealers (Depots)                                                                                      For an automated referral of authorized service outlets in the        U.S.A., phone 1-800-944-9200 OR visit Hoover on-line at               www.hoover.com                                                                                                                              This warranty does not cover pick up, delivery, or house calls;       \nhowever, if you mail your appliance to a Hoover Sales and             Service Center for warranty service, transportation will be paid      one way.                                                                                                                                    While this warranty gives you specific legal rights, you may          also have other rights which vary from state to state.                                                                                      If further assistance is needed, or if there are questions            concerning this warranty or the availability of warranty service      outlets, phone the Hoover Consumer Response Center, Phone 1-330-      499-9499.                                                                                                                                   In Canada, contact Hoover Canada, Burlington, Ontario L7R 4A8,        1-800-263-6376. 21                                                                                                                          Fill in and Save                                                      For your records, enter the model number and serial numbers in        the spaces provided. These numbers are located on the data label      \nPage - 2                                                        N5998                                                                       on the underside of the main body of the cleaner.                     Model No. ____________________________                                Serial No. _____________________________                              Save your sales receipt and attach it to this manual. Proof of        date of purchase may be required for warranty service of your         cleaner.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          ",
                        "referenceNumber": "warrN5998",
                        "selected": true
                    }
                ]
            }

            **Response for an ensemble product**

            {
                "id": "14355e7",
                "name": "Kirsch® Valance Rod",
                "isNew": false,
                "rating": 0,
                "reviewCount": 0,
                "type": "ENSEMBLE",
                "description": "<p>\r\n\tUse a valance rod to add a topper treatment to your draperies. Valance rods are specially designed to project farther from the wall so they will not interfere with draperies.</p>\r\n",
                "recommendationsURL": "http://api.jcpenney.com/v2/products/14355e7/recommendations",
                "images": [
                    {
                        "url": "http://zoom.jcpenney.com/is/image/0900631b80bf855aM.TIF",
                        "type": "PRIMARY",
                        "altText": "Kirsch%C2%AE+Valance+Rod"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/0900631b80bf855aM.TIF",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/0900631b80bf855aM.TIF",
                        "type": "ALTERNATE",
                        "altText": "Kirsch%C2%AE+Valance+Rod"
                    }
                ],
                "prices": [
                    {
                        "max": 35,
                        "min": 13,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 35,
                        "min": 13,
                        "type": "DEFAULT"
                    }
                ]
            }

            **Response for an EOB Lot**

            {
                "type": "FURNITURE",
                "name": "SPENCER FL RL/SL",
                "isNew": false,
                "rating": 0,
                "reviewCount": 0,
                "prices": [
                    {
                        "max": 220,
                        "min": 220,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 130,
                        "min": 130,
                        "type": "SALE"
                    }
                ],
                "skuId": "79059560109"
            }

            **Response for a monogram product**

            {
                "id": "pp5002720035",
                "name": "Stafford® Essentials Broadcloth Dress Shirt - Big & Tall",
                "isNew": false,
                "rating": 4.62,
                "reviewCount": 112,
                "reviewsURL": "http://api.jcpenney.com/v2/products/pp5002720035/reviews",
                "skuId": "53180980315",
                "type": "REGULAR",
                "description": " Stafford® Essentials Everyday dress shirt is a wardrobe staple featuring our commitment to quality and wearability.",
                "recommendationsURL": "http://api.jcpenney.com/v2/products/pp5002720035/recommendations",
                "images": [
                    {
                        "url": "http://zoom.jcpenney.com/is/image/DP0410201317020493M.tif",
                        "type": "PRIMARY",
                        "altText": "Stafford%C2%AE+Essentials+Broadcloth+Dress+Shirt+-+Big+%26+Tall"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81ce5a5bM",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81ce5a5bM",
                        "type": "ALTERNATE",
                        "altText": "Stafford%C2%AE+Essentials+Broadcloth+Dress+Shirt+-+Big+%26+Tall"
                    }
                ],
                "prices": [
                    {
                        "max": 40,
                        "min": 40,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 19.99,
                        "min": 19.99,
                        "type": "SALE"
                    }
                ],
                "vdata": {
                    "footerNote": "For the styles 1, 4, and 5 (3 ltrs), the Last Name Initial is placed in the center of the monogram personalization entries will appear exactly as they are",
                    "type": "MONOGRAM",
                    "vdataOptions": [
                        {
                            "title": "TYPE (MONO/PERSONLZ)",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "PERSONALIZATION TYPE - MUST BE 3 OR 4 (SHIRTS)                        ",
                                    "regularExpression": "[34]"
                                }
                            ],
                            "description": "3=MONOGRAM; 4=PERSONALIZE  (L/S SHIRTS)",
                            "values": [
                                {
                                    "name": "3 - INITIALS",
                                    "value": "3",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3",
                                    "selected": true
                                },
                                {
                                    "name": "4 - NAME",
                                    "value": "4",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=4",
                                    "selected": false
                                }
                            ]
                        },
                        {
                            "title": "THREAD COLOR",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "ALPHABETIC - MUST CONTAIN ALPHA CHARACTERS ONLY                       ",
                                    "regularExpression": "[a-zA-Z]+"
                                }
                            ],
                            "image": {
                                "url": "http://http://www.jcpenney.com/mobile/images/vdata_color_swatch_row.gif",
                                "altText": "THREAD COLOR"
                            },
                            "description": "REFERENCE LIST OF COLORS",
                            "values": [
                                {
                                    "name": "K",
                                    "value": "K",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K",
                                    "selected": true
                                }
                            ]
                        },
                        {
                            "title": "POSITION / LOCATION",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "PLACEMENT - MUST BE L FOR LEFT CUFF, R FOR RIGHT CUFF, OR P FOR POCKET",
                                    "regularExpression": "[LRP]"
                                }
                            ],
                            "description": "L=LEFT CUFF,  R=RIGHT CUFF, OR P=POCKET",
                            "values": [
                                {
                                    "name": "LEFT CUFF",
                                    "value": "L",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L",
                                    "selected": true
                                },
                                {
                                    "name": "RIGHT CUFF",
                                    "value": "R",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=R",
                                    "selected": false
                                },
                                {
                                    "name": "POCKET",
                                    "value": "P",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=P",
                                    "selected": false
                                }
                            ]
                        },
                        {
                            "title": "STYLE NUMBER",
                            "maxRange": 2,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "LETTER STYLE - MUST BE 1 THRU 11                                      ",
                                    "regularExpression": "[1-9]|1[01]|14"
                                }
                            ],
                            "image": {
                                "url": "http://http://www.jcpenney.com/mobile/images/vdata_style_swatch_row.gif",
                                "altText": "STYLE NUMBER"
                            },
                            "description": "PERSONALIZE=6,7,14 /MONOGRAMS =1,2,3,4,5,8,9,10,11",
                            "values": [
                                {
                                    "name": "STYLE 1 IS 2/3 INITIALS",
                                    "value": "1",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=1",
                                    "selected": true
                                },
                                {
                                    "name": "STYLE 10 IS 2/3 INITIALS",
                                    "value": "10",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=10",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 11 IS 3 INITIALS",
                                    "value": "11",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=11",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 14 IS FOR A NAME",
                                    "value": "14",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=14",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 2 IS 3 INITIALS",
                                    "value": "2",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=2",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 3 IS 3 INITIALS",
                                    "value": "3",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=3",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 4 IS 2/3 INITIALS",
                                    "value": "4",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=4",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 5 IS 2/3 INITIALS",
                                    "value": "5",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=5",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 6 IS FOR A NAME",
                                    "value": "6",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=6",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 7 IS FOR A NAME",
                                    "value": "7",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=7",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 8 IS FOR A SINGLE INITIAL",
                                    "value": "8",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=8",
                                    "selected": false
                                },
                                {
                                    "name": "STYLE 9 IS 3 INITIALS",
                                    "value": "9",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=9",
                                    "selected": false
                                }
                            ]
                        },
                        {
                            "title": "FIRST NAME INITIAL",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "ALPHABETIC - MUST CONTAIN ALPHA CHARACTERS ONLY                       ",
                                    "regularExpression": "[a-zA-Z]+"
                                },
                                {
                                    "description": "OPTIONAL - INPUT FIELD DOES NOT REQUIRE ENTRY BY THE CSR              ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "FIRST NAME INITAL FOR MONO(STYLES1,2,3,4,5,9,10,11",
                            "values": [
                                {
                                    "name": "A",
                                    "value": "A",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=1&FIRST%20NAME%20INITIAL=A",
                                    "selected": true
                                }
                            ]
                        },
                        {
                            "title": "MIDDLE NAME INITIAL",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "ALPHABETIC - MUST CONTAIN ALPHA CHARACTERS ONLY                       ",
                                    "regularExpression": "[a-zA-Z]+"
                                },
                                {
                                    "description": "OPTIONAL - INPUT FIELD DOES NOT REQUIRE ENTRY BY THE CSR              ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "MDLE NAME INITAL FOR MONO(STYLES 1,2,3,4,5,9,10,11",
                            "values": [
                                {
                                    "name": "L",
                                    "value": "L",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=1&FIRST%20NAME%20INITIAL=A&MIDDLE%20NAME%20INITIAL=L",
                                    "selected": true
                                }
                            ]
                        },
                        {
                            "title": "LAST NAME INITIAL",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "ALPHABETIC - MUST CONTAIN ALPHA CHARACTERS ONLY                       ",
                                    "regularExpression": "[a-zA-Z]+"
                                },
                                {
                                    "description": "OPTIONAL - INPUT FIELD DOES NOT REQUIRE ENTRY BY THE CSR              ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "SINGLE/LAST NAME INITIAL(STYLES1,2,3,4,5,8,9,10,11",
                            "values": [
                                {
                                    "name": "P",
                                    "value": "P",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002720035?TYPE%20(MONO/PERSONLZ)=3&THREAD%20COLOR=K&POSITION%20/%20LOCATION=L&STYLE%20NUMBER=1&FIRST%20NAME%20INITIAL=A&MIDDLE%20NAME%20INITIAL=L&LAST%20NAME%20INITIAL=P",
                                    "selected": true
                                }
                            ]
                        }
                    ]
                },
                "options": [
                    {
                        "type": "SIZE_RANGE",
                        "name": "SIZE RANGE",
                        "values": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall",
                                "selected": true,
                                "available": true,
                                "value": "Extra Tall"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Big",
                                "selected": false,
                                "available": true,
                                "value": "Big"
                            }
                        ]
                    },
                    {
                        "type": "SKU_OPTION",
                        "name": "NECK SIZE",
                        "values": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16",
                                "selected": true,
                                "available": true,
                                "value": "16"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16.5",
                                "selected": false,
                                "available": true,
                                "value": "16.5"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=17",
                                "selected": false,
                                "available": true,
                                "value": "17"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=17.5",
                                "selected": false,
                                "available": true,
                                "value": "17.5"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=18",
                                "selected": false,
                                "available": true,
                                "value": "18"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=18.5",
                                "selected": false,
                                "available": true,
                                "value": "18.5"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=19",
                                "selected": false,
                                "available": true,
                                "value": "19"
                            }
                        ]
                    },
                    {
                        "type": "SKU_OPTION",
                        "name": "SLEEVE",
                        "values": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=35-36",
                                "selected": true,
                                "available": true,
                                "value": "35-36"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=36-37",
                                "selected": false,
                                "available": false,
                                "value": "36-37"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=37-38",
                                "selected": false,
                                "available": true,
                                "value": "37-38"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=38-39",
                                "selected": false,
                                "available": true,
                                "value": "38-39"
                            }
                        ]
                    },
                    {
                        "name": "SKU_OPTION",
                        "displayText": "COLOR",
                        "optionValues": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=35-36&COLOR=Black",
                                "selected": true,
                                "available": true,
                                "value": "Black",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b81cf057eS.jpg",
                                    "type": "SWATCH",
                                    "altText": "Black"
                                }
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=35-36&COLOR=Blooming%20Blue",
                                "selected": false,
                                "available": true,
                                "value": "Blooming Blue",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b81ce5a1aS.jpg",
                                    "type": "SWATCH",
                                    "altText": "Blooming Blue"
                                }
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=35-36&COLOR=Rock%20Gray",
                                "selected": false,
                                "available": true,
                                "value": "Rock Gray",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b81ce5a1fS.jpg",
                                    "type": "SWATCH",
                                    "altText": "Rock Gray"
                                }
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002720035?SIZE_RANGE=Extra%20Tall&NECK%20SIZE=16&SLEEVE=35-36&COLOR=White",
                                "selected": false,
                                "available": true,
                                "value": "White",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b81ce5a20S.jpg",
                                    "type": "SWATCH",
                                    "altText": "White"
                                }
                            }
                        ]
                    }
                ]
            }

            **Response for a gift card product**

            {
                "id": "1cd63e5",
                "name": "$200 Love Always Gift Card",
                "isNew": false,
                "rating": 0,
                "reviewCount": 0,
                "skuId": "95004590000",
                "type": "GIFTCARD",
                "description": "<p>\r\n\tCelebrate love and happiness. Purchase Gift Cards in any combination you wish.</p>\r\n",
                "recommendationsURL": "http://api.jcpenney.com/v2/products/1cd63e5/recommendations",
                "images": [
                    {
                        "url": "http://zoom.jcpenney.com/is/image/DP0716201212010572M.tif",
                        "type": "PRIMARY",
                        "altText": "%24200+Love+Always+Gift+Card"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81cda42dM",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81cda42dM",
                        "type": "ALTERNATE",
                        "altText": "%24200+Love+Always+Gift+Card"
                    }
                ],
                "prices": [
                    {
                        "max": 200,
                        "min": 200,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 200,
                        "min": 200,
                        "type": "DEFAULT"
                    }
                ],
                "vdata": {
                    "type": "GIFTCARD",
                    "vdataOptions": [
                        {
                            "title": "TO",
                            "maxRange": 27,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "NO CHECKS - NO EDIT RULES APPLY TO THE INPUT FIELD                    ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "NAME OF GIFT CARD RECIPIENT OR DASH - IF BLANK",
                            "values": [
                                {
                                    "name": "Testing",
                                    "value": "Testing",
                                    "url": "http://api.jcpenney.com/v2/products/1cd63e5?TO=Testing",
                                    "selected": true
                                }
                            ]
                        },
                        {
                            "title": "FROM",
                            "maxRange": 27,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "NO CHECKS - NO EDIT RULES APPLY TO THE INPUT FIELD                    ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "NAME OF GIFT CARD GIVER OR DASH - IF BLANK",
                            "values": [
                                {
                                    "name": "Testing",
                                    "value": "Testing",
                                    "url": "http://api.jcpenney.com/v2/products/1cd63e5?FROM=Testing",
                                    "selected": true
                                }
                            ]
                        }
                    ]
                },
                "inventory": {
                    "status": "AVAILABLE",
                    "message": "Available"
                }
            }

            **Response for a hemming product**

            {
                "id": "pp5002690041",
                "name": "Stafford® Essentials Wool Tuxedo Pants – Portly",
                "isNew": false,
                "rating": 0,
                "reviewCount": 0,
                "type": "REGULAR",
                "description": "<p>These wool tuxedo pants mean you&#39;re always ready for special occasions.</p>\r\n",
                "skuId": "55379720018",
                "recommendationsURL": "http://api.jcpenney.com/v2/products/pp5002690041/recommendations",
                "images": [
                    {
                        "url": "http://zoom.jcpenney.com/is/image/0900631b81696fceM.tif",
                        "type": "PRIMARY",
                        "altText": "Stafford%C2%AE+Essentials+Wool+Tuxedo+Pants%C2%A0%E2%80%93%C2%A0Portly"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81e57ae0M",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81e57ae0M",
                        "type": "ALTERNATE",
                        "altText": "Stafford%C2%AE+Essentials+Wool+Tuxedo+Pants%C2%A0%E2%80%93%C2%A0Portly"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81696fceM",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81696fceM",
                        "type": "ALTERNATE",
                        "altText": "Stafford%C2%AE+Essentials+Wool+Tuxedo+Pants%C2%A0%E2%80%93%C2%A0Portly"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81696fcdM",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81696fcdM",
                        "type": "ALTERNATE",
                        "altText": "Stafford%C2%AE+Essentials+Wool+Tuxedo+Pants%C2%A0%E2%80%93%C2%A0Portly"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81696fccM",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/ImageCatalog/0900631b81696fccM",
                        "type": "ALTERNATE",
                        "altText": "Stafford%C2%AE+Essentials+Wool+Tuxedo+Pants%C2%A0%E2%80%93%C2%A0Portly"
                    }
                ],
                "prices": [
                    {
                        "max": 90,
                        "min": 90,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 44.99,
                        "min": 44.99,
                        "type": "SALE"
                    }
                ],
                "options": [
                    {
                        "type": "SKU_OPTION",
                        "name": "WAIST",
                        "values": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=40",
                                "selected": true,
                                "available": true,
                                "value": "40"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=42",
                                "selected": false,
                                "available": true,
                                "value": "42"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=44",
                                "selected": false,
                                "available": true,
                                "value": "44"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=46",
                                "selected": false,
                                "available": true,
                                "value": "46"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=48",
                                "selected": false,
                                "available": true,
                                "value": "48"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=50",
                                "selected": false,
                                "available": true,
                                "value": "50"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=52",
                                "selected": false,
                                "available": true,
                                "value": "52"
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=54",
                                "selected": false,
                                "available": true,
                                "value": "54"
                            }
                        ]
                    },
                    {
                        "type": "SKU_OPTION",
                        "name": "INSEAM",
                        "values": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=40&INSEAM=Unfinished",
                                "selected": true,
                                "available": true,
                                "value": "Unfinished"
                            }
                        ]
                    },
                    {
                        "type": "COLOR_OPTION",
                        "name": "COLOR",
                        "values": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/pp5002690041?WAIST=40&INSEAM=Unfinished&COLOR=Black",
                                "selected": true,
                                "available": true,
                                "value": "Black",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b80c1a612S.jpg",
                                    "type": "SWATCH",
                                    "altText": "Black"
                                }
                            }
                        ]
                    }
                ],
                "vdata": {
                    "type": "HEMMING",
                    "vdataOptions": [
                        {
                            "title": "TAILOR-MADE INSEAM",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "TAYLORING - H=HEM; C=CUFF; U=UNFINISHED                               ",
                                    "regularExpression": "[HCU]"
                                }
                            ],
                            "description": "KEY ONLY: H=HEMMED, C=CUFFED OR U=UNFIN   (PORTLY)",
                            "values": [
                                {
                                    "name": "HEM",
                                    "value": "H",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002690041?TAILOR-MADE%20INSEAM=H",
                                    "selected": "true"
                                },
                                {
                                    "name": "CUFF",
                                    "value": "C",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002690041?TAILOR-MADE%20INSEAM=C",
                                    "selected": "false"
                                },
                                {
                                    "name": "UNFINISHED",
                                    "value": "U",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002690041?TAILOR-MADE%20INSEAM=U",
                                    "selected": "false"
                                }
                            ]
                        },
                        {
                            "title": "HEMMED INSEAM",
                            "maxRange": 2,
                            "minRange": 2,
                            "minValue": 28,
                            "maxValue": 34,
                            "rules": [
                                {
                                    "description": "MIN-MAX WIDTH(LENGTH) - REQUIRES MIN-MAX WIDTH OR LENGTH FOR SETUP    ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "KEY 28-34 WHEN H = HEMMED IS SELECTED",
                            "values": [
                                {
                                    "name": "28",
                                    "value": "28",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002690041?TAILOR-MADE%20INSEAM=H&HEMMED%20INSEAM=28",
                                    "selected": "true"
                                }
                            ]
                        },
                        {
                            "title": "INSEAM - HALF",
                            "maxRange": 3,
                            "minRange": 3,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "OPTIONAL - INPUT FIELD DOES NOT REQUIRE ENTRY BY THE CSR              ",
                                    "regularExpression": "\n\t\t\t"
                                },
                                {
                                    "description": "HALF FRACTION - MUST BE 1/2 ONLY                                      ",
                                    "regularExpression": "1/2"
                                }
                            ],
                            "description": "1/2 TO ADD HALF INCH TO INSEAM LENGTH",
                            "values": [
                                {
                                    "name": "1/2",
                                    "value": "1/2",
                                    "url": "http://api.jcpenney.com/v2/products/pp5002690041?TAILOR-MADE%20INSEAM=H&HEMMED%20INSEAM=28&INSEAM%200%20HALF=1/2",
                                    "selected": "true"
                                }
                            ]
                        }
                    ]
                }
            }

            **Response for a made to measure product**.

            {
                "id": "19145db",
                "name": "jcp home™ Casual Blackout Roman Shade",
                "isNew": false,
                "rating": 0,
                "reviewCount": 0,
                "type": "REGULAR",
                "description": "<p>This custom casual blackout roman shade is a great solution for bedrooms or media rooms.</p>\r\n",
                "recommendationsUrl": "http://api.jcpenney.com/v2/products/19145db/recommendations",
                "skuId": "73910300091",
                "images": [
                    {
                        "url": "http://zoom.jcpenney.com/is/image/DP1117201217551661M.tif",
                        "type": "PRIMARY",
                        "altText": "jcp+home%E2%84%A2+Casual+Blackout+Roman+Shade"
                    },
                    {
                        "url": "http://zoom.jcpenney.com/is/image/DP1117201217551661M.tif",
                        "swatchUrl": "http://zoom.jcpenney.com/is/image/DP1117201217551661M.tif",
                        "type": "ALTERNATE",
                        "altText": "jcp+home%E2%84%A2+Casual+Blackout+Roman+Shade"
                    }
                ],
                "prices": [
                    {
                        "max": 280,
                        "min": 95,
                        "type": "ORIGINAL"
                    },
                    {
                        "max": 168,
                        "min": 57,
                        "type": "SALE"
                    }
                ],
                "options": [
                    {
                        "type": "COLOR_OPTION",
                        "name": "COLOR",
                        "values": [
                            {
                                "url": "http://api.jcpenney.com/v2/products/19145db?COLOR=Burnt%20Henna",
                                "selected": false,
                                "available": true,
                                "value": "Burnt Henna",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b819babafS.jpg",
                                    "type": "SWATCH",
                                    "altText": "Burnt Henna"
                                }
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/19145db?COLOR=Colorado%20Sage",
                                "selected": true,
                                "available": true,
                                "value": "Colorado Sage",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b819babb1S.jpg",
                                    "type": "SWATCH",
                                    "altText": "Colorado Sage"
                                }
                            },
                            {
                                "url": "http://api.jcpenney.com/v2/products/19145db?COLOR=Jackson%20Tan",
                                "selected": false,
                                "available": true,
                                "value": "Jackson Tan",
                                "image": {
                                    "swatchUrl": "http://m.jcpenney.com/mobile/images/0900631b819babb2S.jpg",
                                    "type": "SWATCH",
                                    "altText": "Jackson Tan"
                                }
                            }
                        ]
                    }
                ],
                "vdata": {
                    "type": "MADE_TO_MEASURE",
                    "vdataOptions": [
                        {
                            "title": "WIDTH - WHOLE",
                            "maxRange": 2,
                            "minRange": 2,
                            "minValue": 18,
                            "maxValue": 72,
                            "rules": [
                                {
                                    "description": "MIN-MAX WIDTH(LENGTH) - REQUIRES MIN-MAX WIDTH OR LENGTH FOR SETUP    ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "WIDTH IN WHOLE INCHES       (VARIES FROM 18 TO 72)",
                            "values": [
                                {
                                    "name": "20",
                                    "value": "20",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20",
                                    "selected": "true"
                                }
                            ]
                        },
                        {
                            "title": "WIDTH - FRACTION",
                            "maxRange": 3,
                            "minRange": 3,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "OPTIONAL - INPUT FIELD DOES NOT REQUIRE ENTRY BY THE CSR              ",
                                    "regularExpression": "\n\t\t\t"
                                },
                                {
                                    "description": "EIGHTH FRACTIONS - MUST BE 1/8, 1/4, 3/8, 1/2, 5/8, 3/4, OR 7/8 ONLY  ",
                                    "regularExpression": "(1/8)|(1/4)|(3/8)|(1/2)|(5/8)|(3/4)|(7/8)"
                                }
                            ],
                            "description": "ADDITIONAL WIDTH IN FRACTIONS",
                            "values": [
                                {
                                    "name": "1/8",
                                    "value": "1/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8",
                                    "selected": true
                                },
                                {
                                    "name": "1/4",
                                    "value": "1/4",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/4",
                                    "selected": false
                                },
                                {
                                    "name": "3/8",
                                    "value": "3/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=3/8",
                                    "selected": false
                                },
                                {
                                    "name": "1/2",
                                    "value": "1/2",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/2",
                                    "selected": false
                                },
                                {
                                    "name": "5/8",
                                    "value": "5/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=5/8",
                                    "selected": false
                                },
                                {
                                    "name": "3/4",
                                    "value": "3/4",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=3/4",
                                    "selected": false
                                },
                                {
                                    "name": "7/8",
                                    "value": "7/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=7/8",
                                    "selected": false
                                }
                            ]
                        },
                        {
                            "title": "LENGTH - WHOLE",
                            "maxRange": 2,
                            "minRange": 2,
                            "minValue": 16,
                            "maxValue": 72,
                            "rules": [
                                {
                                    "description": "MIN-MAX WIDTH(LENGTH) - REQUIRES MIN-MAX WIDTH OR LENGTH FOR SETUP    ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "LENGTH IN WHOLE INCHES      (VARIES FROM 16 TO 72)",
                            "values": [
                                {
                                    "name": "16",
                                    "value": "16",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16",
                                    "selected": "true"
                                }
                            ]
                        },
                        {
                            "title": "LENGTH - FRACTION",
                            "maxRange": 3,
                            "minRange": 3,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "OPTIONAL - INPUT FIELD DOES NOT REQUIRE ENTRY BY THE CSR              ",
                                    "regularExpression": "\n\t\t\t"
                                },
                                {
                                    "description": "EIGHTH FRACTIONS - MUST BE 1/8, 1/4, 3/8, 1/2, 5/8, 3/4, OR 7/8 ONLY  ",
                                    "regularExpression": "(1/8)|(1/4)|(3/8)|(1/2)|(5/8)|(3/4)|(7/8)"
                                }
                            ],
                            "description": "ADDITIONAL LENGTH IN FRACTIONS",
                            "values": [
                                {
                                    "name": "1/8",
                                    "value": "1/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=1/8",
                                    "selected": true
                                },
                                {
                                    "name": "1/4",
                                    "value": "1/4",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=1/4",
                                    "selected": false
                                },
                                {
                                    "name": "3/8",
                                    "value": "3/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=3/8",
                                    "selected": false
                                },
                                {
                                    "name": "1/2",
                                    "value": "1/2",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=1/2",
                                    "selected": false
                                },
                                {
                                    "name": "5/8",
                                    "value": "5/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=5/8",
                                    "selected": false
                                },
                                {
                                    "name": "3/4",
                                    "value": "3/4",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=3/4",
                                    "selected": false
                                },
                                {
                                    "name": "7/8",
                                    "value": "7/8",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=7/8",
                                    "selected": false
                                }
                            ]
                        },
                        {
                            "title": "MOUNT",
                            "maxRange": 1,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "CASING - MUST BE I FOR INSIDE OR O FOR OUTSIDE                        ",
                                    "regularExpression": "[IO]"
                                }
                            ],
                            "description": "INSTALLATION: 'I' FOR INSIDE AND 'O' FOR OUTSIDE",
                            "values": [
                                {
                                    "name": "INSIDE",
                                    "value": "I",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=1/8&MOUNT=I",
                                    "selected": true
                                },
                                {
                                    "name": "OUTSIDE",
                                    "value": "O",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=1/8&MOUNT=O",
                                    "selected": false
                                }
                            ]
                        },
                        {
                            "title": "COLOR",
                            "maxRange": 24,
                            "minRange": 1,
                            "minValue": 0,
                            "maxValue": 0,
                            "rules": [
                                {
                                    "description": "NO CHECKS - NO EDIT RULES APPLY TO THE INPUT FIELD                    ",
                                    "regularExpression": "\n\t\t\t"
                                }
                            ],
                            "description": "IF COLOR FIELD BLANK KEY ABBREVIATED COLOR ABOVE",
                            "values": [
                                {
                                    "name": "Colorado Sage",
                                    "value": "Colorado Sage",
                                    "url": "http://api.jcpenney.com/v2/products/19145db?WIDTH%20-%20WHOLE=20&WIDTH%20-%20FRACTION=1/8&LENGTH%20-%20WHOLE=16&LENGTH%20-%20FRACTION=1/8&MOUNT=I&COLOR=Colorado%20Sage",
                                    "selected": true
                                }
                            ]
                        }
                    ]
                }
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Product",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier of the product."
                    },
                    "name": {
                        "type": "string",
                        "description": "Name of the product."
                    },
                    "isNew": {
                        "type": "boolean",
                        "description": "Indicates if the product is a new product.",
                        "default": false
                    },
                    "rating": {
                        "type": "double",
                        "description": "Average ratings for the product.",
                        "default": 0
                    },
                    "reviewCount": {
                        "type": "integer",
                        "description": "Number of reviews for the product.",
                        "default": 0
                    },
                    "reviewsUrl": {
                        "type": "URL",
                        "description": "URL to retrieve the reviews for the product."
                    },
                    "type": {
                        "type": "string",
                        "description": "Product type."
                    },
                    "skuId": {
                        "type": "string",
                        "description": SKU id."
                    },
                    "recommendationsUrl": {
                        "type": "URL",
                        "description": "URL to retrieve the recommendations for the product."
                    },
                    "images": {
                        "title": "List of images assigned to the product.",
                        "type": "array",
                        "items": {
                            "title": "Image",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to the product image."
                                },
                                "swatchUrl": {
                                    "type": "URL",
                                    "description": "URL to the swatch image url for the product."
                                },
                                "type": {
                                    "type": "string",
                                    "enum": [
                                        "PRIMARY",
                                        "ALTERNATE",
                                        "SWATCH"
                                    ],
                                    "description": "Indicates the type of product image."
                                },
                                "altText": {
                                    "type": "string",
                                    "description": "Alternate text for the image."
                                }
                            },
                            "required": [
                                "url",
                                "type"
                            ]
                        }
                    },
                    "prices": {
                        "title": "List of prices for the product.",
                        "type": "array",
                        "items": {
                            "title": "Price",
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "enum": [
                                        "ORIGINAL",
                                        "SALE",
                                        "CLEARANCE",
                                        "MSRP"
                                    ],
                                    "description": "Indicates the type of price."
                                },
                                "min": {
                                    "type": "double",
                                    "description": "Minimum price for the product for the price type",
                                    "default": 0
                                },
                                "max": {
                                    "type": "double",
                                    "description": "Maximum price for the product for the price type.",
                                    "default": 0
                                }
                            },
                            "required": [
                                "type",
                                "min",
                                "max"
                            ]
                        }
                    },
                    "inventory": {
                        "title": "inventory",
                        "type": "object",
                        "properties": {
                            "status": {
                                "type": "string",
                                "description": "Inventory status for the product."
                            },
                            "message": {
                                "type": "string",
                                "description": "Inventory message for the product."
                            }
                        },
                        "required": [
                            "status",
                            "message"
                        ]
                    },
                    "messages": {
                        "title": "List of messages for the product.",
                        "type": "array",
                        "items": {
                            "title": "Message",
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "enum": [
                                        "CHANNEL_MESSAGING",
                                        "PROMOTION",
                                        "TRUCK_DELIVERY"
                                    ],
                                    "description": "Indiates the type of message for the product."
                                },
                                "title": {
                                    "type": "string",
                                    "description": "Message title."
                                },
                                "text": {
                                    "type": "string",
                                    "description": "Complete text of the message."
                                }
                            },
                            "required": [
                                "type",
                                "title",
                                "text"
                            ]
                        }
                    },
                    "description": {
                        "type": "string",
                        "description": "Detailed description of the product. Contains HTML."
                    },
                    "brandUrl": {
                        "type": "URL",
                        "description": "URL to the image for the product brand."
                    },
                    "videoUrl": {
                        "type": "URL",
                        "description": "URL to the product video."
                    },
                    "warranties": {
                        "title": "List of warranties for the product",
                        "type": "array",
                        "items": {
                            "title": "warranty",
                            "type": "object",
                            "properties": {
                                "title": {
                                    "type": "string",
                                    "description": "Title of the warranty assigned to the product."
                                },
                                "description": {
                                    "type": "string",
                                    "description": "Complete description of the warranty. May contain HTML."
                                },
                                "referenceNumber": {
                                    "type": "string",
                                    "description": "Warranty reference number."
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates whether the warranty for the product is selected.",
                                    "default": true
                                }
                            },
                            "required": [
                                "title",
                                "description",
                                "referenceNumber",
                                "selected"
                            ]
                        }
                    },
                    "serviceAgreements": {
                        "title": "List of service agreements.",
                        "type": "array",
                        "items": {
                            "title": "ServiceAgreememt",
                            "type": "object",
                            "properties": {
                                "name": {
                                    "type": "string",
                                    "description": "Name of the service agreement"
                                },
                                "data": {
                                    "type": "string",
                                    "description": "description of the service agreement."
                                },
                                "prices": {
                                    "title": "List of prices",
                                    "type": "array",
                                    "items": {
                                        "title": "Price",
                                        "type": "object",
                                        "properties": {
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "ORIGINAL",
                                                    "SALE",
                                                    "CLEARANCE",
                                                    "MSRP"
                                                ],
                                                "description": "Indicates the type of price."
                                            },
                                            "min": {
                                                "type": "double",
                                                "description": "Minimum price.",
                                                "default": 0
                                            },
                                            "max": {
                                                "type": "double",
                                                "description": "Maximum price",
                                                "default": 0
                                            }
                                        },
                                        "required": [
                                            "page",
                                            "min",
                                            "max"
                                        ]
                                    }
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates whether the service agreement has been selected.",
                                    "default": false
                                },
                                "url": {
                                    "type": "URL",
                                    "description": "URL to service agreement."
                                },
                                "itemId": {
                                    "type": "string",
                                    "description": "Unique identifier for the service agreement."
                                }
                            },
                            "required": [
                                "name",
                                "description",
                                "prices",
                                "selected",
                                "itemId"
                            ]
                        }
                    },
                    "options": {
                        "title": "List of options for the product.",
                        "type": "array",
                        "items": {
                            "title": "Option",
                            "type": "object",
                            "properties": {
                                "name": {
                                    "type": "string",
                                    "description": "Name of the product option"
                                },
                                "type": {
                                    "type": "string",
                                    "enum": [
                                        "DEFAULT",
                                        "COLOR"
                                    ],
                                    "description": "Indicates the type of option."
                                },
                                "values": {
                                    "title": "List of values for the option.",
                                    "type": "array",
                                    "items": {
                                        "title": "OptionValue",
                                        "type": "object",
                                        "properties": {
                                            "url": {
                                                "type": "URL",
                                                "description": "URL to retrieve the details of the product option."
                                            },
                                            "value": {
                                                "type": "string",
                                                "description": "option value string representation."
                                            },
                                            "selected": {
                                                "type": "boolean",
                                                "description": "Indicates that the option value has been selected.",
                                                "default": false
                                            },
                                            "available": {
                                                "type": "boolean",
                                                "description": "Indicates that the option value has been selected.",
                                                "default": false
                                            },
                                            "image": {
                                                "title": "Image",
                                                "type": "object",
                                                "properties": {
                                                    "url": {
                                                        "type": "URL",
                                                        "description": "URL to the product image."
                                                    },
                                                    "swatchUrl": {
                                                        "type": "URL",
                                                        "description": "URL to the product swatch image."
                                                    },
                                                    "type": {
                                                        "type": "string",
                                                        "enum": [
                                                            "PRIMARY",
                                                            "ALTERNATE",
                                                            "SWATCH"
                                                        ],
                                                        "desctiption": "Indicates the type of image."
                                                    },
                                                    "altText": {
                                                        "type": "string",
                                                        "description": "Alternate text for the image."
                                                    }
                                                },
                                                "required": [
                                                    "url",
                                                    "swatchUrl",
                                                    "type",
                                                    "altText"
                                                ]
                                            }
                                        },
                                        "required": [
                                            "url",
                                            "value",
                                            "selected",
                                            "available"
                                        ]
                                    }
                                }
                            },
                            "required": [
                                "name",
                                "type",
                                "values"
                            ]
                        }
                    },
                    "vdata": {
                        "title": "vdata",
                        "type": "object",
                        "properties": {
                            "headerNote": {
                                "type": "string",
                                "description": "VDATA Header note."
                            },
                            "footerNote": {
                                "type": "string",
                                "description": "VDATA footer note."
                            },
                            "type": {
                                "type": "string",
                                "enum": [
                                    "PERSONALIZATION",
                                    "MONOGRAM",
                                    "HEMMING"
                                ],
                                "description": "Indicates the type of VDATA options."
                            },
                            "vdataOptions": {
                                "title": "List of vdata options.",
                                "type": "array",
                                "items": {
                                    "title": "VDATAOption",
                                    "type": "object",
                                    "properties": {
                                        "name": {
                                            "type": "string",
                                            "description": "Name of the VDATA option."
                                        },
                                        "type": {
                                            "type": "String",
                                            "description": "VDATA type"
                                        },
                                        "id" : {
                                            "type": "string",
                                            "description": "VDATA Id."
                                        },
                                        "displayText": {
                                            "type": "string",
                                            "description": "Display text."
                                        },
                                        "maxRange": {
                                            "type": "number"
                                            "description": "Max range."
                                        },
                                        "minRange": {
                                            "type": "number"
                                            "description": "Min range."
                                        },
                                        "maxValue": {
                                            "type": "number"
                                            "description": "Max Value."
                                        },
                                        "minValue": {
                                            "type": "number"
                                            "description": "Min Value."
                                        },
                                        "rules": {
                                            "title": "VData rules.",
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "description": {
                                                        "type": "string",
                                                        "description": "Rule's description."
                                                    },
                                                    "regularExpression": {
                                                        "type": "string",
                                                        "description": "Rule's regular expression."
                                                    }
                                                }
                                            }
                                        },
                                        "image": {
                                            "type": "URL"
                                            "description": "Image URL."
                                        },
                                        "description": {
                                            "type": "string"
                                            "description": "Description."
                                        },
                                        "inputType": {
                                            "type": "string"
                                            "description": "Input type."
                                        },
                                        "values": {
                                            "title": "list of values for vdata option",
                                            "type": "array",
                                            "items": {
                                                "title": "VDATAOptionValue",
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string",
                                                        "description": "Name of the VDATA option value."
                                                    },
                                                    "url": {
                                                        "type": "URL",
                                                        "description": "URL to be used to select the vdata option for the product."
                                                    },
                                                    "selected": {
                                                        "type": "boolean",
                                                        "description": "Indicates that the VDATA option value is selected.",
                                                        "default": false
                                                    }
                                                },
                                                "required": [
                                                    "name",
                                                    "url",
                                                    "selected"
                                                ]
                                            }
                                        }
                                    },
                                    "required": [
                                        "name",
                                        "type",
                                        "displayText",
                                        "maxRange",
                                        "minRange",
                                        "maxValue",
                                        "minValue",
                                        "description",
                                        "inputType"
                                    ]
                                }
                            }
                        },
                        "required": [
                            "headerNote",
                            "footerNote",
                            "type",
                            "vdataOptions"
                        ]
                    }
                },
                "stores": {
                    "title": "List of stores.",
                    "type": "array",
                    "items": {
                        "title": "store",
                        "type": "oject",
                        "properties": {
                            "id": {
                                "type": "string",
                                "description": "Store number."
                            },
                            "name": {
                                "type": "string",
                                "description": "JCPenney store name."
                            },
                            "street": {
                                "type": "string",
                                "description": "Street address of the store."
                            },
                            "city": {
                                "type": "string",
                                "description": "City name."
                            },
                            "stateCode": {
                                "type": "string",
                                "description": "State abbreviation."
                            },
                            "zip": {
                                "type": "string",
                                "description": "zip code of the store."
                            },
                            "phone": {
                                "type": "string",
                                "description": "Formatted phone number of the store."
                            },
                            "distance": {
                                "type": "double",
                                "description": "distance of the store from current location.",
                                "default": 0
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
                                "title": "List of serivces provided by the store.",
                                "type": "array",
                                "items": {
                                    "title": "service",
                                    "type": "string",
                                    "description": "service provided by the JCPenney store."
                                }
                            },
                            "inventory": {
                                "title": "inventory",
                                "type": "object",
                                "properties": {
                                    "status": {
                                        "type": "string",
                                        "description": "Inventory status for the product."
                                    },
                                    "message": {
                                        "type": "string",
                                        "description": "Inventory message for the product."
                                    }
                                },
                                "required": [
                                    "status",
                                    "message"
                                ]
                            },
                            "prices": {
                                "title": "List of prices",
                                "type": "array",
                                "items": {
                                    "title": "price",
                                    "type": "object",
                                    "properties": {
                                        "type": {
                                            "type": "string",
                                            "enum": [
                                                "ORIGINAL",
                                                "SALE",
                                                "CLEARANCE",
                                                "MSRP"
                                            ],
                                            "description": "Type of price"
                                        },
                                        "min": {
                                            "type": "double",
                                            "description": "Minimum price for the product.",
                                            "default": 0
                                        },
                                        "max": {
                                            "type": "double",
                                            "description": "Maximum price for the product.",
                                            "default": 0
                                        }
                                    },
                                    "required": [
                                        "type",
                                        "min",
                                        "max"
                                    ]
                                }
                            }
                        },
                        "required": [
                            "id",
                            "name",
                            "street",
                            "city",
                            "stateCode",
                            "zip",
                            "phone",
                            "distance",
                            "timings",
                            "services",
                            "inventory",
                            "prices"
                        ]
                    },
                    "pages": {
                        "title": "List of page",
                        "type": "array",
                        "items": {
                            "title": "page",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve details of the page."
                                },
                                "number": {
                                    "type": "integer",
                                    "description": "Represents the page number."
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates whether the current page object is selected.",
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
                    "id",
                    "name",
                    "isNew",
                    "rating",
                    "reviewCount",
                    "recommendationsUrl",
                    "prices",
                    "description"
                ]
            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_PAGE_NUMBER_INVALID",
                "errorMessage": "please enter a valid page number."
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

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')


    + Body

            {
                "errorCode": "SRV_PRODUCT_NOTFOUND",
                "errorMessage": "Product not found."
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


## Inventory [/products/{productId}/inventory{?page,pageSize,storeAddress,storeNumber}]
The Inventory resource represents the online/store inventory of the given product.

### Get inventory for a product [GET]
Retrieves the online/store inventory for a product. Supports pagination and sorting for stores result.

+ Parameters
    + productId (required, string, `pp5002310768`) ... Product ID `productId` of the Product (it can be PP, Lot , Ensemble or Sku) to retrieve online and store inventory.
    + page (optional, string, `1`) ... Page Number of the inventory result for store information. Default Value is set to `1`.
    + pageSize (optional, string, `5`) ... Page Size tells how many store results to populate on a single page. Allowed Value Min 5 or Max 10, Default Value is set to `5`.
    + storeAddress (optional, string, `75024/plano,texas/32.767,-117.17`) ... Used for store search based on the zip code/city state/latitude longitude..
    + storeNumber (optional, string, `2795`) ... Retrieve inventory information of a product based on a store number..


+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `Inventory`)

    + Body

            Example of online inventory resource for a product.

            {
                  "status": "BACKODERABLE",
                  "message": "manufacturer shipped (ships in 4 week)"
            }

            Example of store inventory resource for a product.

            {
                "stores": [
                    {
                        "id": "2795",
                        "name": "Stonebriar Mall",
                        "street": "2607 Preston Rd",
                        "city": "Frisco",
                        "stateCode": "TX",
                        "zip": "75034",
                        "phone": " (972) 712-2707",
                        "distance": 1.4,
                        "timings": [
                            {
                                "days": "Mon-Sat",
                                "time": "10:00am-9:00pm"
                            },
                            {
                                "days": "Sun",
                                "time": "11:00am-7:00pm"
                            }
                        ],
                        "services": [
                            "big and tall",
                            "custom decorating",
                            "furniture"
                        ],
                        "inventory": {
                            "status": "INSTOCK",
                            "message": "In stock"
                        }
                    }
                ],
                "pages": [
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5003200163/inventory?storeAddress=75024",
                        "number": 1,
                        "selected": true
                    }
                ]
            }

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Inventory",
                "type": "object",
                "properties": {
                    "title": "Inventory",
                    "type": "object",
                    "properties": {
                        "status": {
                            "type": "string",
                            "description": "Online inventory status for the product."
                        },
                        "message": {
                            "type": "string",
                            "description": "Online inventory status for the product"
                        }
                    },
                    "required": [
                        "status",
                        "message"
                    ]
                },
                "stores": {
                    "title": "List of stores",
                    "type": "array",
                    "items": {
                        "title": "Store",
                        "type": "object",
                        "properties": {
                            "id": {
                                "type": "string",
                                "description": "Unique identifier for the jcpenney store."
                            },
                            "name": {
                                "type": "string",
                                "description": "Name of the JCPenney store."
                            },
                            "street": {
                                "type": "string",
                                "description": "Street addess of the store."
                            },
                            "city": {
                                "type": "string",
                                "description": "City where the JCPenney store is located."
                            },
                            "stateCode": {
                                "type": "string",
                                "description": "State abbreviation of the state where the JCPenney store is located."
                            },
                            "zip": {
                                "type": "string",
                                "description": "Zip code of the JCPenney store."
                            },
                            "phone": {
                                "type": "string",
                                "description": "Formatted string representation of the JCPenney store contact phone number."
                            },
                            "distance": {
                                "type": "double",
                                "description": "distance of the store from current location."
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
                                },
                                "services": {
                                    "title": "List of services provided by the store.",
                                    "type": "array",
                                    "items": {
                                        "title": "service",
                                        "type": "string",
                                        "description": "service provided by the JCPenney store."
                                    }
                                },
                                "inventory": {
                                    "title": "inventory",
                                    "type": "object",
                                    "properties": {
                                        "status": {
                                            "type": "string",
                                            "description": "Inventory status for the product."
                                        },
                                        "message": {
                                            "type": "string",
                                            "description": "Inventory message for the product."
                                        }
                                    },
                                    "required": [
                                        "status",
                                        "message"
                                    ]
                                }
                            },
                            "required": [
                                "id",
                                "name",
                                "street",
                                "city",
                                "stateCode",
                                "zip",
                                "phone",
                                "distance",
                                "timings",
                                "services",
                                "inventory"
                            ]
                        }
                    },
                    "pages": {
                        "title": "List of page objects.",
                        "type": "array",
                        "items": {
                            "title": "Page",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the details of the page."
                                },
                                "number": {
                                    "type": "integer",
                                    "description": "Indicates the page number.",
                                    "default": 1
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates that the current page is selected.",
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
                }
            }


+ Response 400


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            Response when a invalid page is provided in the request.

            {
                "errorCode": "SRV_PAGE_INVALID",
                "errorMessage": "Page number provided is not applicable to the current request."
            }

            Response when the page size provided is invalid.

            {
                "errorCode": "SRV_PAGESIZE_INVALID",
                "errorMessage": "Page size provided is invalid. Only value between 24 and 96 are allowed."
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

+ Response 404


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_PRODUCTS_NOTFOUND",
                "errorMessage": "Product not found."
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


## Price [/products/{productId}/prices{?page,pageSize,storeAddress,storeNumber}]
There are different types of prices for a product in online channel or in JCPenney stores. A product always has atleast 2 prices and can have a maximum of 3 prices associated
to it. The different type of prices available in the system are:

- DEFAULT - Indicates the default active price for the product
- ORIGINAL - Original price of the product.
- SALE - Sale price of the product.
- CLEARANCE - Clearance price of the product.
- MSRP - Manufacturer suggested retail price for the product.


### Get Price. [GET]
This service retrieves the pricing information for a product. The resource may represent the online/store pricing for the product based on the query parameters provided in the request.
Pagination is supported for store price information. Price can be retrieved in different currencies depending on the value of the request header X-Currency.

+ Parameters
    + productId (required, string, `pp5002310768`) ... Product ID or Lot Id or SKU ID of a product to retrieve the Prices.
    + page (optional, string, `1`) ... Page Number of the price result for store information. Default Value is set to `1`.
    + pageSize (optional, string, `5`) ... Page Size tells how many store results to populate on a single page. Allowed Value Min 5 or Max 10, Default Value is set to `5`.
    + storeAddress (optional, string, `75024/plano,texas/32.767,-117.17`) ... Used for store search based on the zip code/city state/latitude longitude..
    + storeNumber (optional, string, `2795`) ... Used to retrieve  inventory information of a product in jcpenney store based on a store number..

+ Request

    + Headers

            X-Currency: required, string, default- USD ... (Used to determine the currency to be used for displaying the price information for the product.)


+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Price[]')

    + Body

            Example to retrieve the online price for product pp5003230750.

            {
                "prices": [
                    {
                        "type": "ORIGINAL",
                        "min": 50,
                        "max": 50
                    },
                    {
                        "type": "SALE",
                        "min": 19.99,
                        "max": 19.99
                    }
                ]
            }

            Example to retrieve the store pricing information for product pp5003230750 in jcpenney stores with zip code 75024

            {
                "stores": [
                    {
                        "id": "2795",
                        "name": "Stonebriar Mall",
                        "street": "2607 Preston Rd",
                        "city": "Frisco",
                        "stateCode": "TX",
                        "zip": "75034",
                        "phone": " (972) 712-2707",
                        "distance": 1.4,
                        "timings": [
                            {
                                "days": "Mon-Sat",
                                "time": "10:00am-9:00pm"
                            },
                            {
                                "days": "Sun",
                                "time": "11:00am-7:00pm"
                            }
                        ],
                        "services": [
                            "big and tall",
                            "custom decorating",
                            "furniture"
                        ],
                        "prices": [
                            {
                                "type": "ORIGINAL",
                                "min": 50,
                                "max": 50
                            },
                            {
                                "type": "SALE",
                                "min": 19.99,
                                "max": 19.99
                            }
                        ]
                    }
                ],
                "pages": [
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5003230750/prices?page=1&pageSize=24",
                        "number": 1,
                        "selected": true
                    }
                ]
            }

    + Schema



            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Prices",
                "type": "object",
                "properties": {
                    "prices": {
                        "title": "List of prices",
                        "type": "array",
                        "items": {
                            "title": "Price",
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "enum": [
                                        "ORIGINAL",
                                        "SALE",
                                        "CLEARANCE",
                                        "MSRP"
                                    ],
                                    "description": "Indicates the type of price."
                                },
                                "min": {
                                    "type": "double",
                                    "description": "Minimum price for the product.",
                                    "default": 0
                                },
                                "max": {
                                    "type": "double",
                                    "description": "maximum price for the product.",
                                    "default": 0
                                }
                            },
                            "required": [
                                "type",
                                "min",
                                "max"
                            ]
                        }
                    },
                    "stores": {
                        "title": "List of stores",
                        "type": "array",
                        "items": {
                            "title": "Store",
                            "type": "object",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier for the jcpenney store."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "JCPenney store name."
                                },
                                "street": {
                                    "type": "string",
                                    "description": "Street address of the JCPenney store."
                                },
                                "city": {
                                    "type": "string",
                                    "description": "city name."
                                },
                                "stateCode": {
                                    "type": "string",
                                    "description": "State abbreviation."
                                },
                                "zip": {
                                    "type": "string",
                                    "description": "Zip code of the JCPenney store."
                                },
                                "phone": {
                                    "type": "string",
                                    "description": "Formatted phone number of the store."
                                },
                                "distance": {
                                    "type": "double",
                                    "description": "distance of the store from current location.",
                                    "default": 0
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
                                },
                                "prices": {
                                    "title": "List of prices",
                                    "type": "array",
                                    "items": {
                                        "title": "price",
                                        "type": "object",
                                        "properties": {
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "ORIGINAL",
                                                    "SALE",
                                                    "CLEARANCE",
                                                    "MSRP"
                                                ],
                                                "description": "Type of price"
                                            },
                                            "min": {
                                                "type": "double",
                                                "description": "Minimum price for the product.",
                                                "default": 0
                                            },
                                            "max": {
                                                "type": "double",
                                                "description": "Maximum price for the product.",
                                                "default": 0
                                            }
                                        },
                                        "required": [
                                            "type",
                                            "min",
                                            "max"
                                        ]
                                    }
                                },
                                "required": [
                                    "id",
                                    "name",
                                    "street",
                                    "city",
                                    "stateCode",
                                    "zip",
                                    "phone",
                                    "distance",
                                    "timings",
                                    "services",
                                    "prices"
                                ]
                            }
                        },
                        "pages": {
                            "title": "List of page",
                            "type": "array",
                            "items": {
                                "title": "page",
                                "type": "object",
                                "properties": {
                                    "url": {
                                        "type": "URL",
                                        "description": "URL to retrieve details of the page."
                                    },
                                    "number": {
                                        "type": "integer",
                                        "description": "Represents the page number."
                                    },
                                    "selected": {
                                        "type": "boolean",
                                        "description": "Indicates whether the current page object is selected.",
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
                    }
                }
            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            Response when a invalid page is provided in the request.

            {
                "errorCode": "SRV_PAGE_INVALID",
                "errorMessage": "Page number provided is not applicable to the current request."
            }

            Response when the page size provided is invalid.

            {
                "errorCode": "SRV_PAGESIZE_INVALID",
                "errorMessage": "Page size provided is invalid. Only value between 24 and 96 are allowed."
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

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_PRODUCTS_NOTFOUND",
                "errorMessage": "Product not found."
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

## Product Recommendations [/products/{productId}/recommendations{?type}]
List of recommended products based on the given product.

### Get recommendations for a product. [GET]
+ Parameters
    + productId (required, string, `pp5002310768`) ... Id of the Product to retrieve all its recommendations.
    + type (optional, string, `PRODUCT`) ... type indicates the location for which recommendations are to be retrieved. Default Value is set to `PRODUCT`.

+ Request

            Example: http://api.jcpenney.com/products/pp5002310768/recommendations

    + Headers

            X-Currency: optional, string, default- USD ... (Used to determine the currency to be used for displaying the price information for the product.)

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Product[]')

    + Body

            [
                {
                    "id": "pp5002961049",
                    "url": "http://api.jcpenney.com/v2/products/pp5002961049",
                    "name": "jcp™ Long-Sleeve Crewneck Tee",
                    "isNew": false,
                    "rating": 0,
                    "reviewCount": 0,
                    "images": [
                        {
                            "url": "http://zoom.jcpenney.com/is/image/DP1104201318163609C.tif",
                            "swatchUrl": "http://zoom.jcpenney.com/is/image/DP1104201318163609C.tif",
                            "type": "PRIMARY",
                            "altText": "jcp™ Long-Sleeve Crewneck Tee"
                        }
                    ],
                    "prices": [
                        {
                            "type": "ORIGINAL",
                            "min": 40,
                            "max": 40
                        },
                        {
                            "type": "SALE",
                            "min": 15.99,
                            "max": 15.99
                        }
                    ]
                }
            ]

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of products",
                "type": "array",
                "items": {
                    "title": "Product",
                    "type": "object",
                    "properties": {
                        "id": {
                            "type": "string",
                            "description": "Unique identifier for the product."
                        },
                        "url": {
                            "type": "URL",
                            "description": "URL to retrieve the complete product information."
                        },
                        "name": {
                            "type": "string",
                            "description": "Name of the product."
                        },
                        "isNew": {
                            "type": "boolean",
                            "description": "Indicates whether the product is a new product.",
                            "default": false
                        },
                        "rating": {
                            "type": "double",
                            "description": "Overall rating for the product.",
                            "default": 0
                        },
                        "reviewCount": {
                            "type": "integer",
                            "description": "Number of reviews for the product.",
                            "default": 0
                        },
                        "images": {
                            "title": "List of images for the product.",
                            "type": "array",
                            "items": {
                                "title": "Image",
                                "type": "object",
                                "properties": {
                                    "url": {
                                        "type": "URL",
                                        "description": "URL to the product image."
                                    },
                                    "swatchUrl": {
                                        "type": "URL",
                                        "description": "URL to the swatch image for the product."
                                    },
                                    "type": {
                                        "type": "string",
                                        "enum": [
                                            "PRIMARY",
                                            "ALTERNATE",
                                            "SWATCH"
                                        ],
                                        "description": "Indicates the type of product image."
                                    },
                                    "altText": {
                                        "type": "string",
                                        "description": "Alternate text for the image."
                                    }
                                },
                                "required": [
                                    "url",
                                    "type"
                                ]
                            }
                        },
                        "prices": {
                            "title": "List of Prices",
                            "type": "array",
                            "items": {
                                "title": "Price",
                                "type": "object",
                                "properties": {
                                    "type": {
                                        "type": "string",
                                        "enum": [
                                            "ORIGINAL",
                                            "SALE",
                                            "CLEARANCE",
                                            "MSRP"
                                        ],
                                        "description": "Indicates the type of price."
                                    },
                                    "min": {
                                        "type": "double",
                                        "description": "Minimum price for the product.",
                                        "default": 0
                                    },
                                    "max": {
                                        "type": "double",
                                        "description": "Maximum price for the product.",
                                        "default": 0
                                    }
                                },
                                "required": [
                                    "type",
                                    "min",
                                    "max"
                                ]
                            }
                        }
                    },
                    "required": [
                        "id",
                        "name",
                        "url",
                        "isNew",
                        "rating",
                        "reviewsCount",
                        "prices"
                    ]
                }
            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')


    + Body

            {
                "errorCode": "SRV_TYPE_INVALID",
                "errorMessage": "Type value is invalid. Possible values [PRODUCT, CART, FAVORITES]"
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

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_PRODUCT_NOTFOUND",
                "errorMessage": "Product not found."
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

## Reviews [/products/{productId}/reviews{?page,pageSize,sortBy}]
Represents the product reviews provided by the customers.

### List all Reviews for a product [GET]

+ Parameters
    + productId (required, string, `pp5002310768`) ... Id of the Product to retrieve all itso associated reviews.
    + page (optional, string, `1`) ... Page Number of the reviews result set. Default Value is set to `1`.
    + pageSize (optional, string, `4`) ... Page Size tells how many reviews to populate on a single page. Allowed Value Range 4-10, Default Value is set to `4`.
    + sortBy (optional, string, `featured reviews`) ... Sorting Option used to sort the results according to the type of the Review. Allowed values range [`featuredreviews, newest, oldest, highestrating, lowestrating, mosthelpful, longest, shortest`]. Default Value set is `featuredreviews`.

+ Request

            Example: http://api.jcpenney.com/products/pp5002310768/reviews?page=2&pageSize=4&sortBy=featuredreviews

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `Reviews`)

    + Body

            {
                "reviews": [
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5002990111/reviews/5002990111",
                        "title": "Cute dress, great price",
                        "text": "I brought this dress to wear to a fall wedding and I loved it. Just add some stylish knee boots and some accessories to dress it up. The material is soft and you will be HOT in this dress, so there's no need to layer underneath. I have back fat rolls and a bit of a belly, but I didn't even need to wear any supportive undergarments to smooth them out - they didn't show at all.",
                        "pros": "Soft material, no need for spanks, great price",
                        "cons": "none so far",
                        "recommend": true,
                        "ratings": [
                            {
                                "name": "OVERALL",
                                "max": 5,
                                "value": 4
                            },
                            {
                                "name": "VALUE",
                                "max": 5,
                                "value": 4
                            },
                            {
                                "name": "FIT",
                                "max": 5,
                                "value": 3.6
                            },
                            {
                                "name": "STYLING",
                                "max": 5,
                                "value": 4.4
                            }
                        ],
                        "customer": {
                            "name": "Ema",
                            "url": "http://reviews.jcpenney.com/profiles/1573-en_us/C0ED7FE04D65982424CEFE996D2B95AF/profile.htm",
                            "from": "Elmont, NY",
                            "age": "25-29",
                            "gender": "FEMALE",
                            "shoppingFrequency": "OCCASIONALLY"
                        }
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5002990111/reviews/5002990112",
                        "title": "very nice dress",
                        "text": "It's a very nice dress that just meet my expectation. The belt is a little bit high to my waist, I'm not sure whether it is just the style, so I just take it out and put it back to where I feel comfortable. It's simple and warm. I'm very satisfied with it.",
                        "pros": "nice color, nice style and nice fabric",
                        "cons": "Belt is kind of higher than my waist",
                        "recommend": true,
                        "ratings": [
                            {
                                "name": "OVERALL",
                                "max": 5,
                                "value": 4
                            },
                            {
                                "name": "VALUE",
                                "max": 5,
                                "value": 4
                            },
                            {
                                "name": "FIT",
                                "max": 5,
                                "value": 4
                            },
                            {
                                "name": "STYLING",
                                "max": 5,
                                "value": 4
                            }
                        ],
                        "customer": {
                            "name": "Kathy",
                            "url": "http://reviews.jcpenney.com/profiles/1573-en_us/E5C6572A78ED0613A155FA5654C95848/profile.htm",
                            "from": "Virginia",
                            "age": "30-39",
                            "gender": "FEMALE",
                            "shoppingFrequency": "FREQUENTLY"
                        }
                    }
                ],
                "pages": [
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5002990111/reviews?sortBy=featuredreviews&page=1&pageSize=4",
                        "number": 1,
                        "selected": true
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5002990111/reviews?sortBy=featuredreviews&page=2&pageSize=4",
                        "number": 2,
                        "selected": false
                    }
                ],
                "sortOptions": [
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5002990111/reviews?sortBy=featuredreviews",
                        "name": "Featured Reviews",
                        "order": 1,
                        "selected": true
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/products/pp5002990111/reviews?sortBy=expertreviews",
                        "name": "Expert Reviews",
                        "order": 2,
                        "selected": false
                    }
                ]
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Reviews",
                "type": "object",
                "properties": {
                    "reviews": {
                        "title": "List of reviews",
                        "type": "array",
                        "items": {
                            "title": "review",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the review information."
                                },
                                "title": {
                                    "type": "string",
                                    "description": "Review title or summary."
                                },
                                "text": {
                                    "type": "string",
                                    "description": "Review text."
                                },
                                "pros": {
                                    "type": "string",
                                    "description": "Pros listed by the user in the review for the product."
                                },
                                "cons": {
                                    "type": "string",
                                    "description": "Cons listed by the user in the review for the product."
                                },
                                "recommend": {
                                    "type": "boolean",
                                    "description": "Indicates whether the review is recommended.",
                                    "default": false
                                },
                                "ratings": {
                                    "title": "List of ratings provided by the user.",
                                    "type": "array",
                                    "items": {
                                        "title": "Rating",
                                        "type": "object",
                                        "properties": {
                                            "name": {
                                                "type": "string",
                                                "description": "Title/Name of the rating."
                                            },
                                            "max": {
                                                "type": "double",
                                                "description": "Max allowed value for the rating",
                                                "default": 5
                                            },
                                            "value": {
                                                "type": "double",
                                                "description": "Rating value provided.",
                                                "default": 0
                                            }
                                        },
                                        "required": [
                                            "name",
                                            "max",
                                            "value"
                                        ]
                                    }
                                },
                                "customer": {
                                    "title": "Customer",
                                    "type": "object",
                                    "properties": {
                                        "name": {
                                            "type": "string",
                                            "description": "Name of the customer who provided the review."
                                        },
                                        "url": {
                                            "type": "URL",
                                            "description": "URL to retrieve the page where the customer information can be viewed."
                                        },
                                        "from": {
                                            "type": "string",
                                            "description": "Location of the user as provided while submitting the review."
                                        },
                                        "age": {
                                            "type": "string",
                                            "enum": [
                                                "UNDER18",
                                                "18-24",
                                                "25-29",
                                                "30-39",
                                                "40-49",
                                                "50-60",
                                                "OVER60"
                                            ],
                                            "description": "string representation of age range of the customer as provided while submitting the review."
                                        },
                                        "gender": {
                                            "type": "string",
                                            "enum": [
                                                "MALE",
                                                "FEMALE"
                                            ],
                                            "description": "Gender of the customer submitting the review."
                                        },
                                        "shoppingFrequency": {
                                            "type": "string",
                                            "enum": [
                                                "FIRSTTIME",
                                                "OCCASIONALLY",
                                                "REGULARLY"
                                            ],
                                            "description": "Indicates the shopping frequency of the customer submitting the review."
                                        }
                                    },
                                    "required": [
                                        "id",
                                        "url",
                                        "from",
                                        "age",
                                        "gender",
                                        "shoppingFrequency"
                                    ]
                                }
                            },
                            "required": [
                                "url",
                                "title",
                                "text",
                                "pros",
                                "cons",
                                "recommend",
                                "ratings"
                            ]
                        }
                    },
                    "pages": {
                        "title": "List of pages",
                        "type": "array",
                        "items": {
                            "title": "Page",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the results for the selected page."
                                },
                                "number": {
                                    "type": "integer",
                                    "description": "Page number",
                                    "default": 1
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates if the current page is selected.",
                                    "default": false
                                }
                            },
                            "required": [
                                "url",
                                "number",
                                "selected"
                            ]
                        }
                    },
                    "sortOptions": {
                        "title": "List of sort options.",
                        "type": "array",
                        "items": {
                            "title": "SortOption",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to sort the reviews result in a particular order."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the sort option."
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates whether the current sort option is selected by the user.",
                                    "default": false
                                },
                                "order": {
                                    "type": "integer",
                                    "description": "Indicates the order of the sort options",
                                    "default": 1
                                }
                            },
                            "required": [
                                "url",
                                "name",
                                "selected",
                                "order"
                            ]
                        }
                    }
                }
            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            Example when the client has requested for an invalid page number.
            {
              "errorCode": "SRV_PAGE_INVALID",
              "errorMessage": "Page number provided is not applicable to the current request."
            }

            Example when page size provided by client is invalid.
            {
              "errorCode": "SRV_PAGESIZE_INVALID",
              "errorMessage": "Page size provided is invalid. Only value between 24 and 96 are allowed."
            }

            Example when an invalid sort by option is provided.
            {
              "errorCode": "SRV_SORTBY_INVALID",
              "errorMessage": "Sort by value provided is invalid. SortBy value should be one of: [featuredreviews, expertreviews, staffreviews, topcontributors, photoreviews, newest, oldest, highestrating, lowestrating, mosthelpful, longest, shortest]"
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


+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_PRODUCT_NOTFOUND",
                "errorMessage": "Product not found."
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

## Review [/product/{productId}/reviews]
### Create a review [POST]
User needs to have a valid session to create/post a review for the product. A user can provide a particular rating for a product, write review and recommend
the product as well.

+ Parameters
    + productId (required, string, `pp5002310768`) ... Id of the Product to submit reviews for.

+ Request (application/json)

    + Body

            {
                "ratings": [
                    {
                        "name": "OVERALL",
                        "value": 4
                    },
                    {
                        "name": "FIT",
                        "value": 4
                    },
                    {
                        "name": "VALUE",
                        "value": 3.6
                    },
                    {
                        "name": "STYLING",
                        "value": 4.4
                    }
                ],
                "recommended": true,
                "summary": "very nice dress",
                "text": "It's a very nice dress that just meet my expectation. The belt is a little bit high to my waist, I'm not sure whether it is just the style, so I just take it out and put it back to where I feel comfortable. It's simple and warm. I'm very satisfied with it.",
                "pros": "nice color, nice style and nice fabric",
                "cons": "Belt is kind of higher than my waist",
                "customer": {
                    "name": "luv2shop",
                    "location": "Virginia",
                    "age": "30-39",
                    "gender": "FEMALE",
                    "shoppingFrequency": "REGULARLY"
                }
            }

    + Schema




            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Review",
                "type": "object",
                "properties": {
                    "ratings": {
                        "title": "List of ratings.",
                        "type": "array",
                        "items": {
                            "title": "Rating",
                            "type": "object",
                            "properties": {
                                "name": {
                                    "type": "string",
                                    "description": "name of the rating for which the rating should be applied."
                                },
                                "value": {
                                    "type": "double",
                                    "description": "rating value.",
                                    "default": 0
                                }
                            },
                            "required": [
                                "name",
                                "value"
                            ]
                        }
                    },
                    "recommended": {
                        "type": "boolean",
                        "description": "Indicates whether the customer has recommended the product.",
                        "default": false
                    },
                    "summary": {
                        "type": "string",
                        "description": "Summary of the review"
                    },
                    "text": {
                        "type": "string",
                        "description": "Text of the product review."
                    },
                    "pros": {
                        "type": "string",
                        "description": "Pros listed by the customer for the product."
                    },
                    "cons": {
                        "type": "string",
                        "description": "Cons listed by the customer for the product."
                    },
                    "customer": {
                        "title": "Customer",
                        "type": "object",
                        "properties": {
                            "name": {
                                "type": "string",
                                "description": "Name of the customer submitting the review."
                            },
                            "location": {
                                "type": "string",
                                "description": "Location of the customer."
                            },
                            "age": {
                                "type": "string",
                                "enum": [
                                    "UNDER18",
                                    "18-24",
                                    "25-29",
                                    "30-39",
                                    "40-49",
                                    "50-60",
                                    "OVER60"
                                ],
                                "description": "Age group of the customer."
                            },
                            "gender": {
                                "type": "string",
                                "enum": [
                                    "MALE",
                                    "FEMALE"
                                ],
                                "description": "Gender of the customer."
                            },
                            "shoppingFrequency": {
                                "type": "string",
                                "enum": [
                                    "FIRSTTIME",
                                    "OCCASIONALLY",
                                    "REGULARLY"
                                ],
                                "description": "shopping frequency of the customer."
                            }
                        },
                        "required": [
                            "name",
                            "location",
                            "age",
                            "gender",
                            "shoppingFrequency"
                        ]
                    }
                },
                "required": [
                    "ratings",
                    "recommended",
                    "summary",
                    "text",
                    "pros",
                    "cons",
                    "customer"
                ]
            }

+ Response 201

    + Headers

                Content-Type: application/json
                Location: (required, URL, 'http://api.jcpenney.com/v2/product/{productId}/reviews/{reviewId}')

    + Body

            {

            }

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')


    + Body

            {
                "errorCode": "SRV_PRODUCT_NOTFOUND",
                "errorMessage": "Product not found."
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

## Review [/product/{productId}/reviews/{reviewId}]
### Get a review [GET]
Review resource matching the reviewId passed in the requested URL

+ Parameters
    + productId (required, string, `pp5002310768`) ... Id of the Product.
    + reviewId  (required, string, `51748189`) ... Id of the review to be retrieved.

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Review')

    + Body

            {
                "title": "Cute dress, great price",
                "text": "I brought this dress to wear to a fall wedding and I loved it. Just add some stylish knee boots and some accessories to dress it up. The material is soft and you will be HOT in this dress, so there's no need to layer underneath. I have back fat rolls and a bit of a belly, but I didn't even need to wear any supportive undergarments to smooth them out - they didn't show at all.",
                "pros": "Soft material, no need for spanks, great price",
                "cons": "none so far",
                "recommend": true,
                "ratings": [
                    {
                        "name": "OVERALL",
                        "max": 5,
                        "value": 4
                    },
                    {
                        "name": "VALUE",
                        "max": 5,
                        "value": 4
                    },
                    {
                        "name": "FIT",
                        "max": 5,
                        "value": 3.6
                    },
                    {
                        "name": "STYLING",
                        "max": 5,
                        "value": 4.4
                    }
                ],
                "customer": {
                    "name": "Ema",
                    "url": "http://reviews.jcpenney.com/profiles/1573-en_us/C0ED7FE04D65982424CEFE996D2B95AF/profile.htm",
                    "from": "Elmont, NY",
                    "age": "25-29",
                    "gender": "FEMALE",
                    "shoppingFrequency": "OCCASIONALLY"
                }
            }

    + Schema

            {
                "schema": "http://json-schema.org/draft-04/schema#",
                "title": "Review",
                "properties": {
                    "title": {
                        "type": "string",
                        "description": "Title of the review."
                    },
                    "text": {
                        "type": "string",
                        "description": "complete review of the product."
                    },
                    "pros": {
                        "type": "string",
                        "description": "Pros of the product."
                    },
                    "cons": {
                        "type": "string",
                        "description": "Cons of the product."
                    },
                    "recommend": {
                        "type": "boolean",
                        "description": "Indicates if the product is recommended by the user.",
                        "default": false
                    },
                    "ratings": {
                        "title": "List of rating for the product",
                        "type": "array",
                        "items": {
                            "title": "Review",
                            "type": "object",
                            "properties": {
                                "name": {
                                    "type": "string",
                                    "description": "Name of the rating."
                                },
                                "max": {
                                    "type": "double",
                                    "description": "max value allowed for the rating.",
                                    "default": 5
                                },
                                "value": {
                                    "type": "double",
                                    "description": "rating value provided by the customer.",
                                    "default": 0
                                }
                            },
                            "required": [
                                "name",
                                "max",
                                "value"
                            ]
                        }
                    },
                    "customer": {
                        "title": "Customer",
                        "type": "object",
                        "properties": {
                            "name": {
                                "type": "string",
                                "description": "Name of the customer who provided the review."
                            },
                            "url": {
                                "type": "URL",
                                "description": "URL to retrieve the page where the customer information can be viewed."
                            },
                            "from": {
                                "type": "string",
                                "description": "Location of the user as provided while submitting the review."
                            },
                            "age": {
                                "type": "string",
                                "enum": [
                                    "UNDER18",
                                    "18-24",
                                    "25-29",
                                    "30-39",
                                    "40-49",
                                    "50-60",
                                    "OVER60"
                                ],
                                "description": "string representation of age range of the customer as provided while submitting the review."
                            },
                            "gender": {
                                "type": "string",
                                "enum": [
                                    "MALE",
                                    "FEMALE"
                                ],
                                "description": "Gender of the customer submitting the review."
                            },
                            "shoppingFrequency": {
                                "type": "string",
                                "enum": [
                                    "FIRSTTIME",
                                    "OCCASIONALLY",
                                    "REGULARLY"
                                ],
                                "description": "Indicates the shopping frequency of the customer submitting the review."
                            }
                        },
                        "required": [
                            "id",
                            "url",
                            "from"
                        ]
                    }
                },
                "required": [
                    "title",
                    "text",
                    "pros",
                    "cons",
                    "recommend",
                    "ratings",
                    "customer"
                ]
            }

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_PRODUCT_NOTFOUND",
                "errorMessage": "Product not found."
            }

            {
                "errorCode": "SRV_REVIEW_NOTFOUND",
                "errorMessage": "Review not found."
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

## Search [/search?{?q,page,pageSize,sortBy,filters}]
List of products returned that matches the search criteria. The search result can be sorted and filtered along with pagination.

### Get Products by Text Search [GET]
Get the products whose name matches the search term.

+ Parameters
    + q (required, string, `shirts`) ... search term.
    + page (optional, Integer, `2`) ... Used for pagination of products.
    + pageSize (optional, Integer, `24`) ... Min 24, Max 96. default: 24. Used to indicate the number of products to be retrieved. If the number of products requested is more than the number of products matching the search criteria then all the products are returned.
    + sortBy (optional, String, `pricehightolow`) ... one of ('bestmatch', 'pricehightolow', 'pricelowtohigh', 'ratingshightolow', 'ratingslowtohigh'). default: 'bestmatch'. Used for sorting the products.
    + filters (optional, String, `1234`) ... Used for facet navigation of products.

+ Request

            Example: http://api.jcpenney.com/v2/search?q=shirts&page=2

    + Headers

            X-Currency: String ... (optional, String, `USD`)

+ Response 200


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, '')

    + Body

            {
                "count": 10,
                "query": "polo shirts",
                "products": [
                    {
                        "id": "pp5002260205",
                        "name": "The Foundry Supply Co.™ Jersey Pocket Polo Shirt – Big & Tall",
                        "url": "http://api.jcpenney.com/v2/products/pp5002260205",
                        "isNew": false,
                        "rating": 0,
                        "reviewCount": 0,
                        "images": [
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP1127201219540167M.tif",
                                "type": "PRIMARY",
                                "altText": "The+Foundry+Supply+Co.%E2%84%A2+Jersey+Pocket+Polo+Shirt%C2%A0%E2%80%93%C2%A0Big+%26+Tall"
                            },
                            {
                                "url": "http://zoom.jcpenney.com/is/image/DP0117201320084850C.tif",
                                "swatchUrl": "http://www.jcpenney.com/dotcom/images/DP1127201219540567S.jpg",
                                "type": "SWATCH",
                                "altText": "Electric Blu/ Navy"
                            }
                        ],
                        "prices": [
                            {
                                "max": 40,
                                "min": 40,
                                "type": "ORIGINAL"
                            },
                            {
                                "max": 14.99,
                                "min": 14.99,
                                "type": "CLEARANCE"
                            }
                        ]
                    },
                    {
                        "id": "1c66271",
                        "name": "French Toast® Piqué Polo Shirt - Boys",
                        "url": "http://api.jcpenney.com/v2/products/1c66271",
                        "isNew": false,
                        "rating": 0,
                        "reviewCount": 0,
                        "images": [
                            {
                                "url": "http://zoom.jcpenney.com/is/image/0900631b81c72a02M.TIF",
                                "type": "PRIMARY",
                                "altText": "French+Toast%C2%AE+Piqu%C3%A9+Polo+Shirt+-+Boys"
                            },
                            {
                                "url": "http://zoom.jcpenney.com/is/image/1c72a02_1c72a0f_412-8200_Black_jpg.tif",
                                "swatchUrl": "http://www.jcpenney.com/dotcom/images/0900631b81c72a0fS.jpg",
                                "type": "SWATCH",
                                "altText": "Black"
                            }
                        ],
                        "prices": [
                            {
                                "max": 11,
                                "min": 11,
                                "type": "ORIGINAL"
                            },
                            {
                                "max": 11,
                                "min": 11,
                                "type": "DEFAULT"
                            }
                        ]
                    }
                ],
                "filters": [
                    {
                        "id": "899",
                        "name": "Team",
                        "type": "DEFAULT",
                        "values": [
                            {
                                "id": "4294964962",
                                "url": "http://api.jcpenney.com/v2/search?q=polo%20shirts&page=1&pageSize=24&filters=4294964962",
                                "name": "not selected",
                                "count": 3,
                                "selected": false,
                                "available": true
                            }
                        ]
                    }
                ],
                "pages": [
                    {
                        "url": "http://api.jcpenney.com/v2/search?q=polo%20shirts&pageNum=1&pageSize=24",
                        "number": 1,
                        "selected": true
                    }
                ],
                "sortOptions": [
                    {
                        "url": "http://api.jcpenney.com/v2/search?q=polo%20shirts&pageSize=24&pageNum=1&sortBy=pricehightolow",
                        "name": "pricehightolow",
                        "selected": false,
                        "order": 2
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/search?q=polo%20shirts&pageSize=24&pageNum=1&sortBy=pricelowtohigh",
                        "name": "pricelowtohigh",
                        "selected": false,
                        "order": 3
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/search?q=polo%20shirts&pageSize=24&pageNum=1&sortBy=ratingshightolow",
                        "name": "ratingshightolow",
                        "selected": false,
                        "order": 4
                    },
                    {
                        "url": "http://api.jcpenney.com/v2/search?q=polo%20shirts&pageSize=24&pageNum=1&sortBy=best%20match",
                        "name": "best match",
                        "selected": true,
                        "order": 1
                    }
                ]
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Products",
                "type": "object",
                "properties": {
                    "query": {
                        "type": "string",
                        "description": "The search term."
                    },
                    "count": {
                        "type": "integer",
                        "description": "Count of number of products.",
                        "default": 0
                    },
                    "products": {
                        "title": "List of products",
                        "type": "array",
                        "description": "Array of products",
                        "items": {
                            "title": "Product",
                            "type": "object",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier of the product."
                                },
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the product detail information."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the product."
                                },
                                "isNew": {
                                    "type": "boolean",
                                    "description": "Indicates that the product is a new product.",
                                    "default": false
                                },
                                "rating": {
                                    "type": "double",
                                    "description": "Average rating of the product.",
                                    "default": 0
                                },
                                "reviewCount": {
                                    "type": "integer",
                                    "description": "Number of reviews for the product",
                                    "default": 0
                                },
                                "images": {
                                    "title": "List of images for the product",
                                    "type": "array",
                                    "items": {
                                        "title": "Image",
                                        "type": "object",
                                        "properties": {
                                            "url": {
                                                "type": "URL",
                                                "description": "URL to the product image."
                                            },
                                            "swatchUrl": {
                                                "type": "URL",
                                                "description": "URL to the swatch image for the product."
                                            },
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "PRIMARY",
                                                    "ALTERNATE",
                                                    "SWATCH"
                                                ],
                                                "description": "Indicates the type of product image."
                                            },
                                            "altText": {
                                                "type": "string",
                                                "description": "Alternate text for the image."
                                            }
                                        },
                                        "required": [
                                            "url",
                                            "type"
                                        ]
                                    }
                                },
                                "prices": {
                                    "title": "List of prices for the product.",
                                    "type": "array",
                                    "items": {
                                        "title": "Price",
                                        "type": "object",
                                        "properties": {
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "ORIGINAL",
                                                    "SALE",
                                                    "CLEARANCE",
                                                    "MSRP"
                                                ],
                                                "description": "Indicates the type of price."
                                            },
                                            "min": {
                                                "type": "double",
                                                "description": "minimum price amount for the product.",
                                                "default": 0
                                            },
                                            "max": {
                                                "type": "double",
                                                "description": "maximum price amount for the product.",
                                                "default": 0
                                            }
                                        },
                                        "required": [
                                            "type",
                                            "min",
                                            "max"
                                        ]
                                    }
                                },
                                "messages": {
                                    "title": "List of messages for the product",
                                    "type": "array",
                                    "items": {
                                        "title": "Message",
                                        "type": "object",
                                        "properties": {
                                            "type": {
                                                "type": "string",
                                                "enum": [
                                                    "CHANNEL_MESSAGING",
                                                    "PROMOTION",
                                                    "TRUCK_DELIVERY"
                                                ],
                                                "description": "Indicates the type of message."
                                            },
                                            "title": {
                                                "type": "string",
                                                "description": "Title of the message"
                                            },
                                            "text": {
                                                "type": "string",
                                                "description": "Detail description of the message."
                                            }
                                        },
                                        "required": [
                                            "type",
                                            "title",
                                            "text"
                                        ]
                                    }
                                }
                            },
                            "required": [
                                "id",
                                "url",
                                "name",
                                "isNew",
                                "rating",
                                "reviewCount",
                                "prices"
                            ]
                        }
                    },
                    "filters": {
                        "title": "Set of filters for facet navigation of products",
                        "type": "array",
                        "items": {
                            "title": "Filter",
                            "type": "object",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier for the filter."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the filter."
                                },
                                "type": {
                                    "type": "string",
                                    "enum": [
                                        "DEFAULT",
                                        "RANGE",
                                        "PRICE_RANGE"
                                    ],
                                    "description": "Indicates the type of filter."
                                },
                                "values": {
                                    "title": "List of filter values which can be applied.",
                                    "type": "array",
                                    "items": {
                                        "title": "FilterValue",
                                        "type": "object",
                                        "properties": {
                                            "id": {
                                                "type": "string",
                                                "description": "Unique identifier for the filter value."
                                            },
                                            "url": {
                                                "type": "URL",
                                                "description": "URL to be used to apply the filter."
                                            },
                                            "name": {
                                                "type": "string",
                                                "description": "Name of the filter value"
                                            },
                                            "image": {
                                                "type": "URL",
                                                "description": "URL to the image assigned to the dimension value."
                                            },
                                            "count": {
                                                "type": "integer",
                                                "description": "Count of products for which the filter value is applicable.",
                                                "default": 0
                                            },
                                            "selected": {
                                                "type": "boolean",
                                                "description": "Indicates whether the current filter value is selected for the product.",
                                                "default": false
                                            },
                                            "available": {
                                                "type": "boolean",
                                                "description": "Indicates whether the current filter value is available for selection.",
                                                "default": true
                                            }
                                        },
                                        "required": [
                                            "id",
                                            "url",
                                            "name",
                                            "image",
                                            "count",
                                            "selected",
                                            "available"
                                        ]
                                    }
                                }
                            },
                            "required": [
                                "id",
                                "name",
                                "type",
                                "values"
                            ]
                        }
                    },
                    "pages": {
                        "title": "Set of pages for supporting pagination",
                        "type": "object",
                        "items": {
                            "title": "page",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to be used to retrieve the products in the required page."
                                },
                                "number": {
                                    "type": "integer",
                                    "description": "Page number",
                                    "default": 1
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates if the current page object is selected.",
                                    "default": false
                                }
                            },
                            "required": [
                                "url",
                                "number",
                                "selected"
                            ]
                        }
                    },
                    "sortOptions": {
                        "title": "List of sort options applicable to the products.",
                        "type": "array",
                        "items": {
                            "title": "SortOption",
                            "type": "object",
                            "properties": {
                                "url": {
                                    "type": "URL",
                                    "description": "URL to be used to retrieve the products sorted in a particular order."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "Name of the sort option."
                                },
                                "selected": {
                                    "type": "boolean",
                                    "description": "Indicates if the sort option is selected.",
                                    "default": false
                                },
                                "order": {
                                    "type": "integer",
                                    "description": "Order of the sort option to be displayed.",
                                    "default": 1
                                }
                            },
                            "required": [
                                "url",
                                "name",
                                "selected",
                                "order"
                            ]
                        }
                    }
                }
            }

+ Response 400
    The request could not be understood by the server due to malformed syntax. The client SHOULD NOT repeat the request without modifications.

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            Request contains an invalid page.

            {
                "errorCode": "SRV_PAGE_INVALID",
                "errorMessage": "Page number provided is not applicable to the current request."
            }

            Request contains invalid page size.

            {
                "errorCode": "SRV_PAGESIZE_INVALID",
                "Page size provided is invalid. Only value between 24 and 96 is allowed."
            }

            Request contains invalid sort option.

            {
                "errorCode": "SRV_SORTBY_INVALID",
                "errorMessage": "Sort by value provided is invalid. SortBy value should be one of: [featured, pricehightolow, pricelowtohigh, ratingshightolow]."
            }

            Request contains an invalid filter value.

            {
                "errorCode": "SRV_FILTER_INVALID",
                "errorMessage": "The filter value provided is not applicable to the current request."
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

## Suggestions [/search/suggestions/{searchTerm}]
### Get suggestions for a search term [GET]
It does a predictive search and returns suggestions to users regarding the search criteria. For example, user types in 'shirts', this service will return--'poloshirts', 'denimshirts', etc.

+ Parameters
   + searchTerm (required, string, `shirts`) ... `searchTerm` is used to retrieve the suggestions.

+ Request

            Example: http://api.jcpenney.com/v2/search/suggestions/shirts

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Suggestions')

    + Body

            {
                "searchTerm": "shirts",
                "count": 5,
                "suggestions": [
                    "shirts",
                    "poloshirts",
                    "sweatshirts",
                    "denimshirts",
                    "womenssweatshirts"
                ]
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Suggestion",
                "type": "object",
                "properties": {
                    "searchTerm": {
                        "type": "string",
                        "description": "The search term."
                    },
                    "count": {
                        "type": "string",
                        "description": "Count of number of search suggestion"
                    },
                    "suggestions": [
                        "type": "string",
                        "description": "List of suggestions"
                    ]
                },
                "required": [
                    "searchTerm",
                    "count",
                    "suggestions"
                ]
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


