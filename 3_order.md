# Group Order
This document explains the bag and checkout functionality. The functionality supported are add items and manage shopping bag, apply & view promotions to the bag, add or update shipping address, shipping option and payment method, add and view gift wrap, review and submit order.
Authenticated user can view their order history as well as individual order details, guest user can only view their placed order by providing phone number for a particular order they had placed.

## Bag items [/cart/items]
### Add to bag [POST]
Add items to the shopping bag. Different kinds of items can be added to the bag including regular merchandise items, gift cards and items with variable data like Monogram or Made to Measure.

+ Request

    + Body


            [
                {
                    "id": "25112010121",
                    "quantity": 2
                },
                {
                    "id": "51315070000",
                    "quantity": 1
                }
            ]


    + Schema


                {
                    "$schema": "http://json-schema.org/draft-04/schema#",
                    "title": "Add item input",
                    "type": "array",
                    "items": {
                        "title": "item input",
                        "type": "object",
                        "properties": {
                            "id": {
                                "type": "string",
                                "description": "11-digit SKU id to be added to the bag."
                            },
                            "quantity": {
                                "type": "integer",
                                "description": "Number of items to be added to the bag."
                            },
                            "attributes": {
                                "type": "array",
                                "title": "List of attributes for the item",
                                "items": {
                                    "title": "Attribute",
                                    "type": "object",
                                    "properties": {
                                        "type": {
                                            "type": "string",
                                            "description": "Type of attribute"
                                        },
                                        "value": {
                                            "type": "string",
                                            "description": "value of the attribute."
                                        }
                                    },
                                    "required": [
                                        "type",
                                        "value"
                                    ]
                                }
                            }
                        },
                        "required": [
                            "id",
                            "quantity"
                        ]
                    }
                }



+ Response 201

    + Headers

            Content-Type: application/json
            Location: (required,URL,'https://api.jcpenney.com/v2/cart/items')


    + Body

            {

            }
    + Schema

            {

            }


+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
              "errorCode": "SRV_ITEM_NOTACTIVE",
              "errorMessage": "Item not found."
            }



    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)
    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }



    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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



### Get item list [GET]
Retrieves a complete list of items which are available in the bag. Each item is identified by its unique commerce ID.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

+ Response 200

    + Headers


            Content-Type: application/json
            X-Data-Type: String ... (required, String)


    + Body

            [
                    {
                        "id": "ci11739009654",
                        "productNumber": "FC513-1507D",
                        "productUrl": "http://api.jcpenney.com/v2/products/5131507",
                        "name": " St. John's Bay® Flannel Shirt",
                        "imageUrl": "https://zoom.jcpenney.com/is/image/DP0729201318152867C.tif",
                        "activePrice": 14.99,
                        "originalPrice": 30,
                        "sale": true,
                        "savings": 15.01,
                        "quantity": 2,
                        "totalWithoutDiscount": 29.98,
                        "total": 29.98,
                        "inventoryStatus": "INSTOCK",
                        "attributes": [
                            {
                                "type": "size",
                                "value": "Medium"
                            },
                            {
                                "type": "color",
                                "value": "Charcoal"
                            }
                        ]
                    },
                    {
                        "id": "ci11739009653",
                        "productNumber": "FC251-1201D",
                        "productUrl": "http://api.jcpenney.com/v2/products/2511201",
                        "name": " Liz Claiborne Ponte Sheath Dress",
                        "imageUrl": "https://zoom.jcpenney.com/is/image/DP1003201318301485C.tif",
                        "activePrice": 35.99,
                        "originalPrice": 60,
                        "sale": true,
                        "savings": 24.01,
                        "quantity": 1,
                        "totalWithoutDiscount": 35.99,
                        "total": 35.99,
                        "inventoryStatus": "INSTOCK",
                        "attributes": [
                            {
                                "type": "size",
                                "value": "8"
                            },
                            {
                                "type": "color",
                                "value": "Black"
                            }
                        ]
                    }
                ]


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "type": "array",
                "title": "list of items in bag",
                "items": {
                            "title": "Item",
                            "type": "object",
                            "properties": {
                            "id": {
                                "type": "string",
                                "description": "unique identifier for the item in the bag."
                            },
                            "productNumber": {
                                "type": "string",
                                "description": "Formatted product number."
                            },
                        "productUrl": {
                            "type": "URL",
                            "description": "URL to the catalog service to retrieve product details."
                        },
                        "productId": {
                            "type": "string",
                            "description": "11-digit SKU id for the item."
                        },
                        "name": {
                            "type": "string",
                            "description": "Name of the product."
                        },
                        "imageUrl": {
                            "type": "string",
                            "description": "URL to the image assigned to the product."
                        },
                        "activePrice": {
                            "type": "double",
                            "description": "active/current price for the product.",
                            "default": 0
                        },
                        "originalPrice": {
                            "type": "double",
                            "description": "original price for the product.",
                            "double": 0
                        },
                        "sale": {
                            "type": "boolean",
                            "description": "Indicates that the product is available on clearance.",
                            "default": false
                        },
                        "savings": {
                            "type": "double",
                            "description": "Savings on the item.",
                            "default": 0
                        },
                        "quantity": {
                            "type": "integer",
                            "description": "Number of items added to the bag",
                            "default": 1
                        },
                        "totalWithoutDiscount": {
                        "type": "double",
                        "description": "Item total without discounts or adjustments.",
                        "default": 0
                        },
                        "adjustmentsTotal": {
                            "type": "double",
                            "description": "Adjustments total for the item.",
                            "default": 0
                        },
                        "adjustments": {
                            "type": "array",
                            "title": "List of adjustments for the item",
                            "items": {
                                "type": "object",
                                "title": "adjustment",
                                "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "type of adjustment",
                                    "enum": [
                                    "COUPON",
                                    "REWARDS"
                                    ]
                                },
                                "code": {
                                "type": "string",
                                "description": "Promotion code/ rewards certificate code"
                                },
                                "amount": {
                                "type": "double",
                                "description": "Reward/promo amount adjusted.",
                                "default": 0
                                },
                                "serialNumber": {
                                "type": "string",
                                "description": "Serial number for reward certificate."
                                }
                            },
                        "required": [
                            "type",
                            "code",
                            "amount"
                        ]
                        }
                    },
                    "total": {
                        "type": "double",
                        "description": "item total.",
                        "default": 0
                    },
                    "inventoryStatus": {
                        "type": "string",
                        "description": "Inventory status of the item."
                    },
                    "attributes": {
                        "type": "array",
                        "title": "List of attributes for the item",
                        "items": {
                            "title": "Attribute",
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "Type of attribute"
                                },
                                "value": {
                                    "type": "string",
                                    "description": "value of the attribute."
                                }
                            },
                            "required": [
                                "type",
                                "value"
                            ]
                        }
                    },
                    "parentId": {
                        "type": "string",
                        "description": "id of the parent item in the bag. Applicable to items with service agreements only."
                    }
                },
                "required": [
                    "id",
                    "name",
                    "activePrice",
                    "originalPrice",
                    "sale",
                    "inventoryStatus",
                    "description",
                    "quantity",
                    "productNumber",
                    "productId",
                    "savings",
                    "totalWithoutDiscount",
                    "adjustmentsTotal",
                    "total"
                ]
                }
            }

+ Response 500

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body



            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }




    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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

## Cart Item [/cart/items/{itemId}]
### Get cart item [GET]
Retrieves an Item details available in bag identified by its unique ID.

+ Parameters

    + itemId (required, String, `ci569000001`) ... An unique identifier of the item.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

+ Response 200

    + Headers


            Content-Type: application/json
            X-Currency: (required, String, `Item`)



    + Body


            {
                "id": "ci11739009653",
                "productNumber": "FC251-1201D",
                "productUrl": "http://api.jcpenney.com/v2/products/2511201",
                "name": " Liz Claiborne Ponte Sheath Dress",
                "imageUrl": "https://zoom.jcpenney.com/is/image/DP1003201318301485C.tif",
                "activePrice": 35.99,
                "originalPrice": 60,
                "sale": true,
                "savings": 24.01,
                "quantity": 1,
                "totalWithoutDiscount": 35.99,
                "total": 35.99,
                "inventoryStatus": "INSTOCK",
                "attributes": [
                {
                    "type": "size",
                    "value": "8"
                },
                {
                    "type": "color",
                    "value": "Black"
                }
                ]
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "type": "object",
                "title": "Item in bag",
                "properties": {
                "id": {
                    "type": "string",
                    "description": "unique identifier for the item in the bag."
                },
                "productNumber": {
                    "type": "string",
                    "description": "Formatted product number."
                },
                "productUrl": {
                    "type": "URL",
                    "description": "URL to the catalog service to retrieve product details."
                },
                "productId": {
                    "type": "string",
                    "description": "11-digit SKU id for the item."
                },
                "name": {
                    "type": "string",
                    "description": "Name of the product."
                },
                "imageUrl": {
                    "type": "string",
                    "description": "URL to the image assigned to the product."
                },
                "activePrice": {
                    "type": "double",
                    "description": "active/current price for the product.",
                    "default": 0
                },
                "originalPrice": {
                    "type": "double",
                    "description": "original price for the product.",
                    "double": 0
                },
                "sale": {
                    "type": "boolean",
                    "description": "Indicates that the product is available on clearance.",
                    "default": false
                },
                "savings": {
                    "type": "double",
                    "description": "Savings on the item.",
                    "default": 0
                },
                "quantity": {
                    "type": "integer",
                    "description": "Number of items added to the bag",
                    "default": 1
                },
                "totalWithoutDiscount": {
                    "type": "double",
                    "description": "Item total without discounts or adjustments.",
                    "default": 0
                },
                "adjustmentsTotal": {
                    "type": "double",
                    "description": "Adjustments total for the item.",
                    "default": 0
                },
                "adjustments": {
                    "type": "array",
                    "title": "List of adjustments for the item",
                    "items": {
                    "type": "object",
                    "title": "adjustment",
                    "properties": {
                        "type": {
                            "type": "string",
                            "description": "type of adjustment",
                            "enum": [
                                "COUPON",
                                "REWARDS"
                            ]
                        },
                        "code": {
                            "type": "string",
                            "description": "Promotion code/ rewards certificate code"
                        },
                        "amount": {
                            "type": "double",
                            "description": "Reward/promo amount adjusted.",
                            "default": 0
                        },
                        "serialNumber": {
                            "type": "string",
                            "description": "Serial number for reward certificate."
                        }
                    },
                    "required": [
                        "type",
                        "code",
                        "amount"
                    ]
                    }
                },
                "total": {
                    "type": "double",
                    "description": "item total.",
                    "default": 0
                },
                "inventoryStatus": {
                    "type": "string",
                    "description": "Inventory status of the item."
                },
                "attributes": {
                    "type": "array",
                    "title": "List of attributes for the item",
                    "items": {
                        "title": "Attribute",
                        "type": "object",
                        "properties": {
                            "type": {
                                "type": "string",
                                "description": "Type of attribute"
                            },
                            "value": {
                                "type": "string",
                                "description": "value of the attribute."
                            }
                        },
                        "required": [
                            "type",
                            "value"
                        ]
                    }
                },
                "parentId": {
                    "type": "string",
                    "description": "id of the parent item in the bag. Applicable to items with service agreements only."
                }
                },
                "required": [
                    "id",
                    "name",
                    "activePrice",
                    "originalPrice",
                    "sale",
                    "inventoryStatus",
                    "description",
                    "quantity",
                    "productNumber",
                    "productId",
                    "savings",
                    "totalWithoutDiscount",
                    "adjustmentsTotal",
                    "total"
                ]
            }




+ Response 404

    + Headers


            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)


    + Body



            {
                "errorCode": "SRV_COMMERCE_ITEMNOTFOUND",
                "errorMessage":  "Item not found for the customer."
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




+ Response 500 (application/json)

    + Headers


            X-Data-Type: (required, String, `ExceptionMessage`)

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




### Update Item [PUT]
Modify/Update an item available in the bag, identified by its unique ID. An update can be in form of changing the item SKU (example color) or quantity.

+ Parameters
   + itemId (required, string, `25112010121`) ... `itemId` is used to update the quantity and item information.
Used to update the item. Item SKU and quantity can be modified.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

    + Body


            {
                 "id": "25112010121",
                 "quantity":  2
            }


    + Schema


              {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Update item input",
                "type": "array",
                "items": {
                  "title": "item input",
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "11-digit SKU id to be added to the bag."
                    },
                    "quantity": {
                      "type": "integer",
                      "description": "Number of items to be added to the bag."
                    },
                    "attributes": {
                      "type": "array",
                      "title": "List of attributes for the item",
                      "items": {
                        "title": "Attribute",
                        "type": "object",
                        "properties": {
                          "type": {
                              "type": "string",
                              "description": "Type of attribute"
                            },
                          "value": {
                            "type": "string",
                            "description": "value of the attribute."
                          }
                        },
                        "required": [
                          "type",
                          "value"
                        ]
                      }
                    }
                  },
                  "required": ["id", "quantity"]
                }
              }



+ Response 200

    + Headers

            Content-Type: application/json
            Location: (required,URL,'https://api.jcpenney.com/v2/cart')


    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, Error`)

    + Body


            {
                    "errorCode": "SRV_ITEM_NOTACTIVE",
                    "errorMessage": "The item is not active and cannot be added to bag."
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
                    "required": ["errorCode", "errorMessage"]
                   }


+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, Error`)

    + Body


            {
                    "errorCode": "SRV_COMMERCE_ITEMNOTFOUND",
                    "errorMessage": "Item not found for the customer."
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
                    "required": ["errorCode", "errorMessage"]
                   }



+ Response 500

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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
                    "required": ["errorCode", "errorMessage"]
                   }



### Delete Item [DELETE]
Removes an item from the bag. The item is identified by its unique ID.

+ Parameter
    + itemId (required, String, `ci524000003`) ... Item ID `itemId` to remove that item from the bag.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json


    + Body

            {

            }
    + Schema

            {

            }

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_COMMERCE_ITEMNOTFOUND",
                "errorMessage": "Commerce item could not be found."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




## Promotions [/cart/promotions]

### Apply Promotion [POST]
Applies promotions to the bag. It supports two type of promotions- Coupons and Rewards.
A promotion can return percentage off / dollar off on the order, or a discount in shipping charges.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

    + Body

            Example applying a promo code to order/bag:
            [
              {
                "type": "COUPON",
                "code": "SHOPDEC"
              }
            ]

            Example to apply a reward certificate to order/bag:
            [
              {
                "type": "REWARDS",
                "code": "3431234435453",
                "serialNumber": "4534234"
              }
            ]


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of promotions to be applied",
                "type": "array",
                "items": {
                    "type": "object",
                    "title": "Promotion",
                    "properties": {
                        "type": {
                            "type": "string",
                            "description": "Indicates the type of promotion",
                            "enum": [
                                "COUPON",
                                "REWARDS"
                            ]
                        },
                        "code": {
                            "type": "string",
                            "description": "Promo code or reward certificate code."
                        },
                        "serialNumber": {
                            "type": "string",
                            "description": "Serial number for reward certificate."
                        }
                    },
                    "required": [
                        "code",
                        "type"
                    ]
                }
            }



+ Response 201

    + Headers


            Content-Type: application/json
            Location: URL ('https://api.jcpenney.com/v2/cart/promotions',required)



    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            Example when the promo code applied is invalid:
            {
              "errorCode": "SRV_PROMOCODE_INVALID",
              "errorMessage": "Enter a valid code."
            }

            Example when the reward requires a serial number:
            {
              "errorCode": "SRV_SERIALNUMBER_NOTAPPLIED",
              "errorMessage": "Enter a valid serial number."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




### Get Promotions [GET]
Retrieves all the promotions applied to the bag.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

+ Response 200

    + Headers


            Content-Type: application/json
            X-Data-Type: (required, String, `Promotion[]`)


    + Body


            [
                {
                    "id": "pc4534523",
                    "type": "COUPON",
                    "code": "SHOPDEC"
                },
                {
                    "id": "rw942342432",
                    "type": "REWARD",
                    "code": "32132132132131",
                    "serialNumber": "43453"
                }
            ]


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of promotions to be applied",
                "type": "array",
                "items": {
                    "type": "object",
                    "title": "Promotion",
                    "properties": {
                        "type": {
                            "type": "string",
                            "description": "Indicates the type of promotion",
                            "enum": [
                                "COUPON",
                                "REWARDS"
                            ]
                        },
                        "code": {
                            "type": "string",
                            "description": "Promo code or reward certificate code."
                        },
                        "serialNumber": {
                            "type": "string",
                            "description": "Serial number for reward certificate."
                        }
                    },
                    "required": [
                        "code",
                        "type"
                    ]
                }
            }




+ Response 500

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERR",
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




## Promotion [/cart/promotions/{promotionId}]
### Get a promotion [GET]
Retrieve details of a particular promotion on a order. The promotion is identified by a unique ID.

+ Parameters

    + promotionId (required, String, `11000002 `) ... An unique identifier of the promotion.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

+ Response 200


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `Promotion`)


    + Body


            {
                "id": "pc12312321",
                "type": "COUPON",
                "code": "SHOPDEC"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Promotion",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier to identify a promotion on order."
                    },
                    "type": {
                        "type": "string",
                        "description": "Indicates the type of promotion",
                        "enum": [
                            "COUPON",
                            "REWARDS"
                        ]
                    },
                    "code": {
                        "type": "string",
                        "description": "Promo code or reward certificate code."
                    },
                    "serialNumber": {
                        "type": "string",
                        "description": "Serial number for reward certificate."
                    }
                },
                "required": [
                    "code",
                    "type"
                ]
            }




+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_PROMOTION_NOTFOUND",
                "errorMessage": "The promotion could not be found."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

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




### Remove Promotion [DELETE]
Deletes a coupon or reward certificate applied to the bag. It is identified by a unique ID.

+ Parameter
    + promotionId (required, String, `12313`) ... Promotion ID `promotionId` to remove from the bag.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json


    + Body

            {

            }
    + Schema

            {

            }

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_PROMOTION_NOTFOUND",
                "errorMessage": "Promotion could not be found."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




## Shipping Address [/cart/shipping/address]
### Add/Update Shipping Address [PUT]
Create or update a shipping address where the items will be shipped. A customer can select store shipping or a regular address. A regular address can have variations in forms of US contiguous/ non-contiguous states or Military Shipping (APO/FPO/DPO).
This operation can only be performed over secure protocol.
##### HTTPS required

+ Request


    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

    + Body


            Example to apply a US address to order

            {
              "firstName": "Alice",
              "lastName": "Sampleton",
              "phone": "8185551234",
              "addressLine1": "5555 Mulholland Drive",
              "city": "Los Angeles",
              "state": "CA",
              "zip": "90068",
              "country": "US",
              "store": false
            }

            Example to apply a store shipping address
            {
              "firstName": "Alice",
              "lastName": "Sampleton",
              "phone": "8185551234",
              "storeNumber": "5601",
              "store": true
            }


    + Schema


            {
                    "$schema": "http://json-schema.org/draft-04/schema#",
                    "title": "Shipping address on order",
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Unique identifier for the address record in the application."
                      },
                      "firstName": {
                        "type": "string",
                        "description": "First name for the customer address.",
                        "minLength": 1,
                        "maxLength": 17
                      },
                      "middleInitial": {
                        "type": "string",
                        "description": "Middle initial for the customer address.",
                        "minLength": 1,
                        "maxLength": 1
                      },
                      "lastName": {
                        "type": "string",
                        "description": "Last name for the customer address.",
                        "minLength": 1,
                        "maxLength": 24
                      },
                      "company": {
                        "type": "string",
                        "description": "Company name for the customer address.",
                        "minLength": 1,
                        "maxLength": 23
                      },
                      "addressLine1": {
                        "type": "string",
                        "description": "Street address line 1.",
                        "minLength": 1,
                        "maxLength": 40
                      },
                      "addressLine2": {
                        "type": "string",
                        "description": "Street address line 2.",
                        "minLength": 0,
                        "maxLength": 40
                      },
                      "addressLine3": {
                        "type": "string",
                        "description": "Street address line 3. Applicable for international address only.",
                        "minLength": 0,
                        "maxLength": 40
                      },
                      "city": {
                        "type": "string",
                        "description": "City name.",
                        "minLength": 1,
                        "maxLength": 20
                      },
                      "APO_FPO_DPO": {
                        "type": "string",
                        "description": "Indicates the type of Military address",
                        "enum": ["APO", "FPO", "DPO"]
                      },
                      "state": {
                        "type": "string",
                        "description": "State code/abbreviation for US.",
                        "maxLength": 2
                      },
                      "province": {
                        "type": "string",
                        "description": "Province/Territory/Region. Province code for Canada address.",
                        "maxLength": 10
                      },
                      "zip": {
                        "type": "string",
                        "description": "zip code.",
                        "maxLength": 8
                      },
                      "country": {
                        "type": "string",
                        "description": "Country code."
                      },
                      "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number",
                        "maxLength": 10
                      },
                      "secondaryPhoneNumber": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number. Applicable to international address only."
                      },
                      "store": {
                        "type": "boolean",
                        "description": "indicates whether the address is a store address",
                        "default": false
                      },
                      "storeNumber": {
                        "type": "string",
                        "description": "JCPenney store number unique identifier."
                      }
                    }
              }



+ Response 200


    + Headers

            Content-Type: application/json

    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, Error`)

    + Body


                Example when first name is not provided
                {
                  "errorCode": "SRV_ORDER_FIRSTNAMEISNULL",
                  "errorMessage": "Enter a valid first name."
                }

                Example when last name is not provided
                {
                  "errorCode": "SRV_ORDER_LASTNAMEISNULL",
                  "errorMessage": "Enter a valid last name."
                }

                Example when phone number is not provided
                {
                  "errorCode": "SRV_ORDER_PHONENUMISNULL",
                  "errorMessage": "Enter a valid phone number."
                }

                Example when address provided is not standardized.
                {
                  "errorCode": "SRV_ORDER_ADDRESSNOTSTANDARDIZED",
                  "errorMessage": "The address you entered is not in standardized format. Please double check that all your information is correct before continuing."
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
                    "required": ["errorCode", "errorMessage"]
                   }



+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, Error`)

    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




### Get Shipping Address [GET]
Retrieves all the Shipping Information on order based on the shipping id. It includes regular and store addresses both.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

   + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, Address`)


    + Body


            {
                "firstName": "Alice",
                "middleInitial": "L",
                "lastName": "Sampleton",
                "addressLineOne": "5701 Scrugg's way",
                "addressLineTwo": "Legacy Village",
                "city": "Los Angeles",
                "state": "CA",
                "zip": "90068",
                "country": "US",
                "phone": "8185551234",
                "store": false
            }



    + Schema


            {
                    "$schema": "http://json-schema.org/draft-04/schema#",
                    "title": "Shipping address on order",
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Unique identifier for the address record in the application."
                      },
                      "firstName": {
                        "type": "string",
                        "description": "First name for the customer address.",
                        "minLength": 1,
                        "maxLength": 17
                      },
                      "middleInitial": {
                        "type": "string",
                        "description": "Middle initial for the customer address.",
                        "minLength": 1,
                        "maxLength": 1
                      },
                      "lastName": {
                        "type": "string",
                        "description": "Last name for the customer address.",
                        "minLength": 1,
                        "maxLength": 24
                      },
                      "company": {
                        "type": "string",
                        "description": "Company name for the customer address.",
                        "minLength": 1,
                        "maxLength": 23
                      },
                      "addressLine1": {
                        "type": "string",
                        "description": "Street address line 1.",
                        "minLength": 1,
                        "maxLength": 40
                      },
                      "addressLine2": {
                        "type": "string",
                        "description": "Street address line 2.",
                        "minLength": 0,
                        "maxLength": 40
                      },
                      "addressLine3": {
                        "type": "string",
                        "description": "Street address line 3. Applicable for international address only.",
                        "minLength": 0,
                        "maxLength": 40
                      },
                      "city": {
                        "type": "string",
                        "description": "City name.",
                        "minLength": 1,
                        "maxLength": 20
                      },
                      "APO_FPO_DPO": {
                        "type": "string",
                        "description": "Indicates the type of Military address",
                        "enum": ["APO", "FPO", "DPO"]
                      },
                      "state": {
                        "type": "string",
                        "description": "State code/abbreviation for US.",
                        "maxLength": 2
                      },
                      "province": {
                        "type": "string",
                        "description": "Province/Territory/Region. Province code for Canada address.",
                        "maxLength": 10
                      },
                      "zip": {
                        "type": "string",
                        "description": "zip code.",
                        "maxLength": 8
                      },
                      "country": {
                        "type": "string",
                        "description": "Country code."
                      },
                      "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number",
                        "maxLength": 10
                      },
                      "secondaryPhoneNumber": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number. Applicable to international address only."
                      },
                      "store": {
                        "type": "boolean",
                        "description": "indicates whether the address is a store address",
                        "default": false
                      },
                      "storeNumber": {
                        "type": "string",
                        "description": "JCPenney store number unique identifier."
                      }
                    }
              }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, Error`)

    + Body


            {
                    "errorCode": "SRV_SESSION_INVALID",
                    "errorMessage": "The customer session is invalid."
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
                    "required": ["errorCode", "errorMessage"]
            }



+ Response 500

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




## Shipping Options [/cart/shipping/options]
### Update Shipping Options [PUT]
Applies a shipping method/option on the order. These options are based on the address which is selected for shipping.
Different shipping charges are applicable for different options. For example- Standard Shipping can be free, while there could be some charges for express or truck-able shipping.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

    + Body


            Example to apply `Economy` shipping option to order.
            {
                "type": "ECONOMY"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Shipping Option",
                "type": "object",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of shipping option selected by customer."
                    }
                },
                "required": [
                    "type"
                ]
            }



+ Response 200

    + Headers

            Content-Type: application/json

    + Body

            {

            }
    + Schema

            {

            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




### Get Shipping Options [GET]
Retrieve list of all shipping options which are available for a particular shipping address.
A flag is available which will indicate which shipping method is selected.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ShippingOption`)


    + Body


            {
                    "shippingOption": [
                        {
                            "type": "STANDARD",
                            "charge": 8,
                            "duration": "4-7 business days",
                            "selected":"true"
                        },
                        {
                            "type": "EXPRESS_ECONOMY",
                            "charge": 15,
                            "duration": "3 business days",
                            "selected":"false"
                        },
                        {
                            "type": "EXPRESS",
                            "charge": 25,
                            "duration": "2 business days",
                            "selected":"false"
                        }
                    ]
                }



    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "type": "array",
                "title": "List of shipping options for the order.",
                "items": {
                    "type": "object",
                    "title": "shipping option",
                    "properties": {
                        "type": {
                            "type": "string",
                            "description": "Type of shipping option"
                        },
                        "charge": {
                            "type": "double",
                            "description": "shipping option charge",
                            "default": 0
                        },
                        "duration": {
                            "type": "string",
                            "description": "shipping duration"
                        },
                        "message": {
                            "type": "string",
                            "description": "Message for the shipping option"
                        },
                        "selected": {
                            "type": "boolean",
                            "description": "Indicates whether the shipping option has been selected by the customer.",
                            "default": false
                        }
                    },
                    "required": [
                        "type",
                        "charge",
                        "duration",
                        "selected"
                    ]
                }
            }




+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




## Gift Wrapping [/cart/giftWrapping]
### Add Gift Wrapping [POST]
Adds gift wrapping for items in the bag. Only the eligible items are allowed to be gift-wrapped.
A customer can create multiple gift-wrapped packages for multiple items in the bag and each package is identified by its unique ID.
Customer can also attach a personalized message on the gift-wrapped package.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

    + Body


            [
                {
                    "itemIds": [
                        "ci12312312",
                        "ci343411231"
                    ],
                    "giftWrapType": "HANDWRAPBOX",
                    "to": "API",
                    "from": "Testing",
                    "personalizedMessage": "HAPPY HOLIDAYS"
                }
            ]


    + Schema


                {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "type": "array",
                "title": "list of gift wraps for items in bag",
                "items": {
                    "title": "gift wrap",
                    "type": "object",
                    "properties": {
                        "itemIds": {
                            "type": "array",
                            "title": "list of items to be gift wrapped.",
                            "items": {
                                "title": "item id",
                                "type": "string"
                            }
                        },
                        "to": {
                            "type": "string",
                            "description": "gift recipient details."
                        },
                        "from": {
                            "type": "string",
                            "description": "gifter details"
                        },
                        "personalizedMessage": {
                            "type": "string",
                            "description": "personalized message for the gift wrap."
                        },
                        "giftWrapType": {
                            "type": "string",
                            "description": "type of gift wrap."
                        }
                    },
                    "required": [
                        "itemIds",
                        "giftWrapType"
                    ]
                }
            }




+ Response 201

    + Headers

            Content-Type: application/json
            Location: (required,URL,'https://api.jcpenney.com/v2/bag/giftWrapping')


    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body

            The item provided is not eligible for gift wrap.
            All items provided are not eligible for gift wrap.
            Example:
            {
                "errorCode": "SRV_GIFTWRAP_INVALID",
                "errorMessage": "The items are not eligible for gift wrap."
            }

            One or more items provided are not eligible for gift wrap.
            Example:
            {
                "errorCode": "SRV_GIFTWRAP_NOT_ELIGIBLE",
                "errorMessage": "The items ci12312312, ci343411231 are not eligible for gift wrap."
            }

            The provided gift wrap type is invalid.
            Example:
            {
                "errorCode": "SRV_GIFTWRAP_TYPE_INVALID",
                "errorMessage": "The gift wrap type is invalid."
            }



    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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




+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)
    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)
    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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




### Get Gift Wrapping [GET]
Retrieves all the gift-wrapped packages on the order.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `GiftWrap`)

    + Body




            [
                {
                    "giftWrapId": "gp231231",
                    "itemIds": [
                        "ci12312312",
                        "ci343411231"
                    ],
                    "giftWrapType": "HANDWRAPBOX",
                    "to": "API",
                    "from": "Testing",
                    "personalizedMessage": "HAPPY HOLIDAYS"
                }
            ]


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "type": "array",
                "title": "list of gift wraps for items in bag",
                "items": {
                    "title": "gift wrap",
                    "type": "object",
                    "properties": {
                        "giftWrapId": {
                            "type": "string",
                            "description": "unique identifier for a gift wrap in the application."
                        },
                        "itemIds": {
                            "type": "array",
                            "title": "list of items to be gift wrapped.",
                            "items": {
                                "title": "item id",
                                "type": "string"
                            }
                        },
                        "to": {
                            "type": "string",
                            "description": "gift recipient details."
                        },
                        "from": {
                            "type": "string",
                            "description": "gifter details"
                        },
                        "personalizedMessage": {
                            "type": "string",
                            "description": "personalized message for the gift wrap."
                        },
                        "giftWrapType": {
                            "type": "string",
                            "description": "type of gift wrap."
                        }
                    },
                    "required": [
                        "giftWrapId",
                        "itemIds",
                        "giftWrapType"
                    ]
                }
            }




+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customers session is invalid."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: (required, String, `ExceptionMessage`)

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





## Gift Wrapping Item [/cart/giftWrapping/{giftWrappingId}]
### Get Gift Wrapping for Item [GET]
Retrieves a single gift-wrapped package associated with a order. It is identified by its unique giftWrappingId.
##### HTTPS required

+ Parameters

    + giftWrappingId (required, String, `11000002 `) ... An unique identifier of the gift wrap.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `GiftWrap`)

    + Body


            {
                "giftWrapId": "gp231231",
                "itemIds": [
                    "ci12312312",
                    "ci343411231"
                ],
                "giftWrapType": "HANDWRAPBOX",
                "to": "API",
                "from": "Testing",
                "personalizedMessage": "HAPPY HOLIDAYS"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "gift wrap",
                "type": "object",
                "properties": {
                    "giftWrapId": {
                        "type": "string",
                        "description": "unique identifier for a gift wrap in the application."
                    },
                    "itemIds": {
                        "type": "array",
                        "title": "list of items to be gift wrapped.",
                        "items": {
                            "title": "item id",
                            "type": "string"
                        }
                    },
                    "to": {
                        "type": "string",
                        "description": "gift recipient details."
                    },
                    "from": {
                        "type": "string",
                        "description": "gifter details"
                    },
                    "personalizedMessage": {
                        "type": "string",
                        "description": "personalized message for the gift wrap."
                    },
                    "giftWrapType": {
                        "type": "string",
                        "description": "type of gift wrap."
                    }
                },
                "required": [
                    "giftWrapId",
                    "itemIds",
                    "giftWrapType"
                ]
            }




+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GIFTWRAP_NOTFOUND",
                "errorMessage": "Gift wrap not found."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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




### Update Gift Wrap for Item [PUT]
Modifies or Edits the contents of the gift wrap in a bag. Edit can be in form of adding/removing items from the package or changing the personalized message.
##### HTTPS required

+ Parameters

    + giftWrappingId (required, String, `11000002 `) ... An unique identifier of the gift wrap.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

    + Body


            {
                "itemIds": [
                    "ci12312312",
                    "ci343411231"
                ],
                "giftWrapType": "HANDWRAPBOX",
                "to": "API",
                "from": "Testing",
                "personalizedMessage": "HAPPY HOLIDAYS"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Gift wrap",
                "properties": {
                    "itemIds": {
                        "type": "array",
                        "title": "list of items to be gift wrapped.",
                        "items": {
                            "title": "item id",
                            "type": "string"
                        }
                    },
                    "to": {
                        "type": "string",
                        "description": "gift recipient details."
                    },
                    "from": {
                        "type": "string",
                        "description": "gifter details"
                    },
                    "personalizedMessage": {
                        "type": "string",
                        "description": "personalized message for the gift wrap."
                    },
                    "giftWrapType": {
                        "type": "string",
                        "description": "type of gift wrap."
                    }
                },
                "required": [
                    "itemIds",
                    "giftWrapType"
                ]
            }





+ Response 200

    + Headers

            Content-Type: application/json

    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

    + Headers


            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GIFTWRAP_INVALID",
                "errorMessage": "The items are not eligible for gift wrap."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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




+ Response 401

    + Headers


            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)


    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GIFTWRAP_NOTFOUND",
                "errorMessage": "Gift wrap not found."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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




### Remove Gift Wrap from Item [DELETE]
Deletes a gift wrap package in bag. It is identified by its unique ID.
##### HTTPS required

+ Parameters

    + giftWrappingId (required, String, `11000002 `) ... An unique identifier of the gift wrap.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json

    + Body

            {

            }
    + Schema

            {

            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)


    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
            }

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GIFTWRAP_NOTFOUND",
                "errorMessage": "Gift wrap not found."
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }

            Schema:
            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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




## Payment Methods [/cart/paymentMethods]
### Create Payment Method [POST]
Creates and applies a payment method to order. Two kinds of payment methods are supported which are Credit Cards and Gift Cards.
System will do the basic validations such as Gift Card balance validation or for Credit Card validity.
##### HTTPS required

+ Request (application/json)

   + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

   + Body


            Example to apply a credit card to order.

                    {
                        "type": "MASTERCARD",
                        "cardNumber": "9999999999999999",
                        "expiryYear": 2014,
                        "expiryMonth": 1,
                        "address": {
                                "id": "addr31566431",
                                "firstName": "Alice",
                                "lastName": "Sampleton",
                                "addressLineOne": "5555 Mulholland Drive",
                                "city": "Los Angeles",
                                "state": "CA",
                                "zip": "90068",
                                "country": "US",
                                "phone": "8185551234"
                            }
                    }



            Example to apply a gift card to order.

                    {
                        "type": "GIFTCARD",
                        "cardNumber": "99999999999999999",
                        "id": "1234"
                    }



    + Schema

                  {
                    "$schema": "http://json-schema.org/draft-04/schema#",
                    "type": "object",
                    "title": "Payment option",
                        "properties": {
                            "idNumber": {
                            "type": "string",
                            "description": "id number for gift cards."
                        },
                        "type": {
                        "type": "string",
                        "description": "Type of card",
                        "enum": [
                            "MASTERCARD",
                            "Visa",
                            "AMEX",
                            "DISCOVER",
                            "JCP",
                            "GIFTCARD"
                                ]
                        },
                        "lastFour": {
                        "type": "string",
                        "description": "Last 4 characters of a card. In case of JCP cards characters 6-10 of the card number.",
                        "minLength": 4,
                        "maxLength": 4
                        },
                        "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month of the card.",
                        "minimum": 1,
                        "maximum": 12
                        },
                        "expiryYear": {
                            "type": "integer",
                            "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date."
                        },
                        "default": {
                            "type": "boolean",
                            "description": "Indicates whether the card is the default payment method for the customer account.",
                            "default": false
                        },
                        "address": {
                            "title": "Address",
                            "type": "object",
                            "properties": {
                        "id": {
                            "type": "string",
                            "description": "Unique identifier for the address record in the application."
                        },
                        "firstName": {
                            "type": "string",
                            "description": "First name for the customer address.",
                            "minLength": 1,
                            "maxLength": 17
                        },
                        "middleInitial": {
                            "type": "string",
                            "description": "Middle initial for the customer address.",
                            "minLength": 1,
                            "maxLength": 1
                        },
                        "lastName": {
                            "type": "string",
                            "description": "Last name for the customer address.",
                            "minLength": 1,
                            "maxLength": 24
                        },
                        "company": {
                            "type": "string",
                            "description": "Company name for the customer address.",
                            "minLength": 1,
                            "maxLength": 23
                        },
                        "addressLineOne": {
                            "type": "string",
                            "description": "Street address line 1.",
                            "minLength": 1,
                            "maxLength": 40
                        },
                        "addressLineTwo": {
                            "type": "string",
                            "description": "Street address line 2.",
                            "minLength": 0,
                            "maxLength": 40
                        },
                        "addressLineThree": {
                            "type": "string",
                            "description": "Street address line 3. Applicable for international address only.",
                            "minLength": 0,
                            "maxLength": 40
                        },
                        "city": {
                            "type": "string",
                            "description": "City name.",
                            "minLength": 1,
                            "maxLength": 20
                        },
                        "militaryAddressType": {
                            "type": "string",
                            "description": "Indicates the type of Military address",
                            "enum": [
                                "APO",
                                "FPO",
                                "DPO"
                            ]
                        },
                        "state": {
                            "type": "string",
                            "description": "State code/abbreviation for US.",
                            "maxLength": 2
                        },
                        "province": {
                            "type": "string",
                            "description": "Province/Territory/Region. Province code for Canada address.",
                            "maxLength": 10
                        },
                        "zip": {
                            "type": "string",
                            "description": "zip code.",
                            "maxLength": 8
                        },
                        "country": {
                            "type": "string",
                            "description": "Country code."
                        },
                        "phone": {
                            "type": "string",
                            "description": "Unformatted 10 digit phone number",
                            "maxLength": 10
                        },
                        "secondaryPhoneNumber": {
                            "type": "string",
                            "description": "Unformatted 10 digit phone number. Applicable to international address only."
                        }
                    },
                    "required": [
                        "country",
                        "firstName",
                        "lastName",
                        "addressLineOne",
                        "city",
                        "state",
                        "zip",
                        "phone"
                        ]
                    }
                },
            "required": [
                "id",
                "type",
                "lastFour",
                "default",
                "address"
                ]
            }





+ Response 200

    + Headers

            Content-Type: application/json

    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: String... (required, String, `ExceptionMessage`)

    + Body

            The input provided is incorrect or not sufficient.
            Example when credit card number is not valid.

                {
                    "errorCode": "SRV_ORDER_CREDITCARDINVALID",
                    "errorMessage": "Enter a valid credit card number."
                }


                Example when expiry month is not provided

                {
                    "errorCode": "SRV_ORDER_EXPIRYMONTH",
                    "errorMessage": "Enter a valid expiry month."
                }


                Example when expiry year is not provided.
                {
                    "errorCode": "SRV_ORDER_EXPIRYYEAR",
                    "errorMessage": "Enter a valid expiry year."
                }


                Example when cvv number is not provided for VISA cards
                {
                    "errorCode": "SRV_ORDER_CVVINVALID",
                    "errorMessage": "Enter a valid CVV number"
                }


                Example when gift card number is not valid.
                {
                    "errorCode": "SRV_ORDER_GCINVALID",
                    "errorMessage": "Enter a valid 19 digit gift card number."
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
            X-Data-Type: String... (required, String, `ExceptionMessage`)

    + Body


            {
                        "errorCode": "SRV_SESSION_INVALID",
                        "errorMessage": "The customer session is invalid."
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
            X-Data-Type: String... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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

### Get Payment Methods [GET]
Retrieves all the Payment Methods applied on order. If two Gift cards and a credit card is applied on the order, this method will return all the three.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'PaymentMethods[]')

    + Body


                    [
                        {
                        "id": "pg343423423",
                        "type": "MASTERCARD",
                        "lastFour": "9999",
                        "expiryYear": 2014,
                        "expiryMonth": 1,
                        "address": {
                            "id": "addr2345311",
                            "firstName": "Alice",
                            "lastName": "Sampleton",
                            "addressLine1": "5555 Mulholland Drive",
                            "city": "Los Angeles",
                            "state": "CA",
                            "zip": "90068",
                            "country": "US",
                            "phone": "8185551234"
                            },
                        {
                            "type": "GIFTCARD",
                            "lastFour": "9999"
                        }
                    ]



    + Schema


                   {
                "title": "List of payment methods ",
                "type": "array",
                "items": {
                "type": "object",
                "title": "Payment option",
                    "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier for the payment method."
                        },
                    "type": {
                        "type": "string",
                        "description": "Type of card",
                        "enum": [
                            "MASTERCARD",
                            "Visa",
                            "AMEX",
                            "DISCOVER",
                            "JCP"
                            ]
                        },
                        "lastFour": {
                        "type": "string",
                        "description": "Last 4 characters of a card. In case of JCP cards characters 6-10 of the card number.",
                        "minLength": 4,
                        "maxLength": 4
                        },
                        "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month of the card.",
                        "minimum": 1,
                        "maximum": 12
                        },
                        "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date."
                        },
                        "default": {
                        "type": "boolean",
                        "description": "Indicates whether the card is the default payment method for the customer account.",
                        "default": false
                        },
                        "address": {
                        "title": "Address",
                        "type": "object",
                        "properties": {
                        "id": {
                        "type": "string",
                        "description": "Unique identifier for the address record in the application."
                        },
                        "firstName": {
                        "type": "string",
                        "description": "First name for the customer address.",
                        "minLength": 1,
                        "maxLength": 17
                        },
                        "middleInitial": {
                        "type": "string",
                        "description": "Middle initial for the customer address.",
                        "minLength": 1,
                        "maxLength": 1
                        },
                        "lastName": {
                        "type": "string",
                        "description": "Last name for the customer address.",
                        "minLength": 1,
                        "maxLength": 24
                        },
                        "company": {
                        "type": "string",
                        "description": "Company name for the customer address.",
                        "minLength": 1,
                        "maxLength": 23
                        },
                        "addressLineOne": {
                        "type": "string",
                        "description": "Street address line 1.",
                        "minLength": 1,
                        "maxLength": 40
                        },
                        "addressLineTwo": {
                        "type": "string",
                        "description": "Street address line 2.",
                        "minLength": 0,
                        "maxLength": 40
                        },
                        "addressLineThree": {
                        "type": "string",
                        "description": "Street address line 3. Applicable for international address only.",
                        "minLength": 0,
                        "maxLength": 40
                        },
                        "city": {
                        "type": "string",
                        "description": "City name.",
                        "minLength": 1,
                        "maxLength": 20
                        },
                        "militaryAddressType": {
                        "type": "string",
                        "description": "Indicates the type of Military address",
                        "enum": [
                            "APO",
                            "FPO",
                            "DPO"
                        ]
                        },
                        "state": {
                        "type": "string",
                        "description": "State code/abbreviation for US.",
                        "maxLength": 2
                        },
                        "province": {
                        "type": "string",
                        "description": "Province/Territory/Region. Province code for Canada address.",
                        "maxLength": 10
                        },
                        "zip": {
                        "type": "string",
                        "description": "zip code.",
                        "maxLength": 8
                        },
                        "country": {
                        "type": "string",
                        "description": "Country code."
                        },
                        "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number",
                        "maxLength": 10
                        },
                        "secondaryPhoneNumber": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number. Applicable to international address only."
                        }
                    },
                    "required": [
                        "country",
                        "firstName",
                        "lastName",
                        "addressLineOne",
                        "city",
                        "state",
                        "zip",
                        "phone"
                    ]
                }
            },
                "required": [
                    "id",
                    "type",
                    "last4",
                    "default",
                    "address"
                ]
                }
            }






+ Response 401

        The customer needs to be authenticated to perform this operation. DPSecureCookie value provided does not match the value in the session.

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                    "errorCode": "SRV_SESSION_INVALID",
                    "errorMessage": "The customer session is invalid."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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


## Payment Method [/cart/paymentMethods/{paymentMethodId}]
### Get Payment Method [GET]
Retrieves a particular payment method identified by its unique ID.
##### HTTPS required

+ Parameters

    + paymentMethodId (required, string, `pg14110233`) ... Payment Method Id `paymentMethodId` of the order.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String... (required, String, `PaymentMethod`)

    + Body


                    {
                    "id": "pg12678657",
                    "type": "MASTERCARD",
                    "cardNumber": "9999999999999999",
                    "expiryYear": 2014,
                    "expiryMonth": 1,
                    "address": {
                        "id": "addr31566431",
                        "firstName": "Alice",
                        "lastName": "Sampleton",
                        "addressLineOne": "5555 Mulholland Drive",
                        "city": "Los Angeles",
                        "state": "CA",
                        "zip": "90068",
                        "country": "US",
                        "phone": "8185551234"
                        }
                    }



    + Schema


                   {
                    "$schema": "http://json-schema.org/draft-04/schema#",
                    "type": "object",
                    "title": "Payment option",
                    "properties": {
                    "id": {
                    "type": "string",
                    "description": "Unique identifier for the payment method"
                    },
                    "type": {
                    "type": "string",
                    "description": "Type of card",
                    "enum": [
                        "MASTERCARD",
                        "Visa",
                        "AMEX",
                        "DISCOVER",
                        "JCP",
                        "GIFTCARD"
                        ]
                    },
                    "lastFour": {
                        "type": "string",
                        "description": "Last 4 characters of a card. In case of JCP cards characters 6-10 of the card number.",
                        "minLength": 4,
                        "maxLength": 4
                        },
                    "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month of the card.",
                        "minimum": 1,
                        "maximum": 12
                        },
                    "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date."
                        },
                    "default": {
                        "type": "boolean",
                        "description": "Indicates whether the card is the default payment method for the customer account.",
                        "default": false
                        },
                    "address": {
                        "title": "Address",
                        "type": "object",
                    "properties": {
                        "id": {
                        "type": "string",
                        "description": "Unique identifier for the address record in the application."
                            },
                    "firstName": {
                        "type": "string",
                        "description": "First name for the customer address.",
                        "minLength": 1,
                        "maxLength": 17
                        },
                    "middleInitial": {
                        "type": "string",
                        "description": "Middle initial for the customer address.",
                        "minLength": 1,
                        "maxLength": 1
                        },
                    "lastName": {
                        "type": "string",
                        "description": "Last name for the customer address.",
                        "minLength": 1,
                        "maxLength": 24
                        },
                    "company": {
                        "type": "string",
                        "description": "Company name for the customer address.",
                        "minLength": 1,
                        "maxLength": 23
                        },
                    "addressLineOne": {
                        "type": "string",
                        "description": "Street address line 1.",
                        "minLength": 1,
                        "maxLength": 40
                        },
                    "addressLineTwo": {
                        "type": "string",
                        "description": "Street address line 2.",
                        "minLength": 0,
                        "maxLength": 40
                        },
                    "addressLineThree": {
                        "type": "string",
                        "description": "Street address line 3. Applicable for international address only.",
                        "minLength": 0,
                        "maxLength": 40
                        },
                    "city": {
                        "type": "string",
                        "description": "City name.",
                        "minLength": 1,
                        "maxLength": 20
                        },
                    "militaryAddressType": {
                        "type": "string",
                        "description": "Indicates the type of Military address",
                        "enum": [
                            "APO",
                            "FPO",
                            "DPO"
                        ]
                        },
                    "state": {
                        "type": "string",
                        "description": "State code/abbreviation for US.",
                        "maxLength": 2
                        },
                    "province": {
                        "type": "string",
                        "description": "Province/Territory/Region. Province code for Canada address.",
                        "maxLength": 10
                        },
                    "zip": {
                        "type": "string",
                        "description": "zip code.",
                        "maxLength": 8
                        },
                    "country": {
                        "type": "string",
                        "description": "Country code."
                        },
                    "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number",
                        "maxLength": 10
                        },
                    "secondaryPhoneNumber": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number. Applicable to international address only."
                        }
                    },
                    "required": [
                        "country",
                        "firstName",
                        "lastName",
                        "addressLineFour",
                        "city",
                        "state",
                        "zip",
                        "phone"
                        ]
                    }
                },
                "required": [
                        "id",
                        "type",
                        "lastFour",
                        "default",
                        "address"
                        ]
                        }






+ Response 404

        The payment method is not found or not available for the customer to view.

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                    "errorCode": "SRV_PAYMENTMETHOD_NOTFOUND",
                    "errorMessage": "Payment method not found."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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

### Update Payment Method [PUT]
Updates a Payment Method identified by its unique ID. An updated can be in form of new credit card type, expiry date change, etc.
##### HTTPS required

+ Parameters

    + paymentMethodId (required, string, `pg14110233`) ... Payment Method Id `paymentMethodId` of the order.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

    + Body

            {
                "type": "MASTERCARD",
                "cardNumber": "9999999999999999",
                "expiryYear": 2014,
                "expiryMonth": 1,
                "addressId": "addr31566431"
            }
    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifer for the payment method"
                    },
                    "type": {
                        "type": "string",
                        "description": "Type of card",
                        "enum": [
                            "MASTERCARD",
                            "Visa",
                            "AMEX",
                            "DISCOVER",
                            "JCP",
                            "GIFTCARD"
                        ]
                    },
                    "last4": {
                        "type": "string",
                        "description": "Last 4 charcters of a card. In case of JCP cards characters 6-10 of the card number",
                        "minLength": "4",
                        "maxLength": "4"
                    },
                    "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month of the card",
                        "minimum": "1",
                        "maximum": "12"
                    },
                    "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date"
                    },
                    "default": {
                        "type": "booelan",
                        "description": "Indicates whether the card is the default payment method for the customer account",
                        "default": "false"
                    },
                    "address":{
                        "title": "ExceptionMessage",
                        "type": "object",
                        "properties": {
                            "id": {
                                "type": "string",
                                "description": "Unique identifer for the payment method"
                            },
                            "firstName": {
                                "type": "string",
                                "description": "First name for the customer address",
                                "minLength": "1",
                                "maxLength": "17"
                            },
                            "middleInitial": {
                                "type": "string",
                                "description": "Middle initial for the customer address",
                                "minLength": "1",
                                "maxLength": "1"
                            },
                            "lastName": {
                                "type": "string",
                                "description": "Last name for the customer address",
                                "minLength": "1",
                                "maxLength": "24"
                            },
                            "company": {
                                "type": "string",
                                "description": "Company name for the customer address",
                                "minLength": "1",
                                "maxLength": "23"
                            },
                            "addressLine1": {
                                "type": "string",
                                "description": "Street address line 1",
                                "minLength": "1",
                                "maxLength": "40"
                            },
                            "addressLine2": {
                                "type": "string",
                                "description": "Street address line 2",
                                "minLength": "1",
                                "maxLength": "40"
                            },
                            "addressLine3": {
                                "type": "string",
                                "description": "Street address line 3.Applicable for international address only",
                                "minLength": "1",
                                "maxLength": "40"
                            },
                            "city": {
                                "type": "string",
                                "description": "City name",
                                "minLength": "1",
                                "maxLength": "20"
                            },
                            "APO_FPO_DPO": {
                                "type": "string",
                                "description": "Indicates the type of Military address",
                                "enum": [
                                     "APO",
                                     "FPO",
                                     "DPO"
                                ]
                            },
                            "state": {
                                "type": "string",
                                "description": "State code/abbreviation for US",
                                "maxLength": "2"
                            },
                            "province": {
                                "type": "string",
                                "description": "Province/Teritory/Region. Province code for Canada address",
                                "maxLength": "10"
                            },
                            "zip": {
                                "type": "string",
                                "description": "zip code",
                                "maxLength": "8"
                            },
                            "country": {
                                "type": "string",
                                "description": "Country code"
                            },
                            "phone": {
                                "type": "string",
                                "description": "Unformatted 10 digit phone number",
                                "maxLength": "10"
                            },
                            "secondaryPhoneNumber": {
                                "type": "string",
                                "description": "Unformatted 10 digit phone number. Appicable to international address only"
                            }
                        },
                        "required": [
                                "country",
                                "firstName",
                                "lastName",
                                "addressLine1",
                                "city",
                                "state",
                                "zip",
                                "phone"
                        ]
                    }
                },
                "required": [
                    "id",
                    "type",
                    "last4",
                    "default",
                    "address"
                ]
            }


+ Response 200


    + Headers

            Content-Type: application/json

    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

        The required mandatory field is not provided.


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_ADDRESS_INVLAID",
                "errorMessage": "Please enter a valid billing address"
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

        The payment method is not found or not available for the customer to view.


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body

            The input provided is incorrect or not sufficient.
            {
                    "errorCode": "SRV_PAYMENTMETHOD_NOTFOUND",
                    "errorMessage": "Payment method not found."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_GENERIC_ERROR",
                "errorMessage": "There was an error while processing your request. Please try after some time."
            }

    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "ExceptionMessage",
                "type": "object",
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


### Delete Payment Method [DELETE]
Deletes a Payment Method identified by unique ID. Only a Gift Card can be deleted with this method, credit card cannot be deleted.
##### HTTPS required

+ Parameters

    + paymentMethodId (required, string, `pg14110233`) ... Payment Method Id `paymentMethodId` of the order.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json

    + Body

            {

            }
    + Schema

            {

            }

+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                    "errorCode": "SRV_PAYMENTMETHOD_NOTFOUND",
                    "errorMessage": "Payment method not found."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

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






## Order Email [/cart/paymentMethods/email]
### Update Order Email [PUT]
Applies the email address to which the Order Confirmation is to be sent for Guest Customers. For registered customers, the email address provided on the JCPenney customer account will be utilized.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

    + Body


            {
                "email": "betty@example.com"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Order Email address",
                "type": "object",
                "properties": {
                    "email": {
                        "type": "string",
                        "description": "Email address to which the order information is to be sent."
                    }
                },
                "required": [
                    "email"
                ]
            }



+ Response 200

    + Headers

            Content-Type: application/json
            Location: (required, URL, 'http://api.jcpenney.com/v2/cart/paymentMethods/email')

    + Body

            {

            }
    + Schema

            {

            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer session is invalid."
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



+ Response 403

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_COMMERCE_OPERATIONFORBIDDEN",
                "errorMessage": "The operation is forbidden for registered customers."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




### Get email [GET]
Retrieves email associated to the current order.
##### HTTPS required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String... (required, String, `Email`)

    + Body


            {
                        "email": "betty@example.com"
            }


    + Schema

                    {
                        "$schema": "http://json-schema.org/draft-04/schema#",
                        "title": "Order Email address",
                        "type": "object",
                        "properties": {
                            "email": {
                                "type": "string",
                                "description": "Email address to which the order information is to be sent."
                            }
                        },

                        "required": [
                            "email"
                        ]
                    }


+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                    "errorCode": "SRV_SESSION_INVALID",
                    "errorMessage": "The customer's session is invalid."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

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






## Order Review and Submit [/cart]
### Get Order Details in the Session [GET]
Retrieves order details for the current session. This will return all the items available in the bag, its Shipping Address and Method, Gift Wrap, Payment Method.

+ Request

    + Headers

            X-Currency: (String, default:`USD`)
            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

   + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `Order`)
    + Body


            Example of retrieving the order details using HTTP Protocol
            http://api.jcpenney.com/v2/cart

            {
                "count": 3,
                "total": 65.97,
                "roundUp": false,
                "itemSubTotal": 65.97,
                "subTotal": 65.97,
                "estimatedShippingCharges": [
                    {
                        "type": "SHIP_TO_HOME",
                        "charge": 8
                    },
                    {
                        "type": "SHIP_TO_STORE",
                        "charge": 0
                    }
                ],
                "items": [
                    {
                        "id": "ci11739009654",
                        "productNumber": "FC513-1507D",
                        "productUrl": "http://api.jcpenney.com/v2/products/5131507",
                        "name": " St. John's Bay?Flannel Shirt",
                        "imageUrl": "https://zoom.jcpenney.com/is/image/DP0729201318152867C.tif",
                        "activePrice": 14.99,
                        "originalPrice": 30,
                        "sale": true,
                        "savings": 15.01,
                        "quantity": 2,
                        "totalWithoutDiscount": 29.98,
                        "total": 29.98,
                        "inventoryStatus": "INSTOCK",
                        "attributes": [
                            {
                                "type": "size",
                                "value": "Medium"
                            },
                            {
                                "type": "color",
                                "value": "Charcoal"
                            }
                        ]
                    },
                    {
                        "id": "ci11739009653",
                        "productNumber": "FC251-1201D",
                        "productUrl": "http://api.jcpenney.com/v2/products/2511201",
                        "name": " Liz Claiborne Ponte Sheath Dress",
                        "imageUrl": "https://zoom.jcpenney.com/is/image/DP1003201318301485C.tif",
                        "activePrice": 35.99,
                        "originalPrice": 60,
                        "sale": true,
                        "savings": 24.01,
                        "quantity": 1,
                        "totalWithoutDiscount": 35.99,
                        "total": 35.99,
                        "inventoryStatus": "INSTOCK",
                        "attributes": [
                            {
                                "type": "size",
                                "value": "8"
                            },
                            {
                                "type": "color",
                                "value": "Black"
                            }
                        ]
                    }
                ]
            }

            Example of order with shipping address and promotion when executed using HTTPS protocol
            https://api.jcpenney.com/v2/cart

            {
                "count": 3,
                "total": 56.07,
                "roundUp": false,
                "itemSubTotal": 65.97,
                "adjustmentsTotal": 9.9,
                "subTotal": 56.07,
                "adjustments": [
                    {
                        "type": "COUPON",
                        "code": "SHOPDEC",
                        "amount": 9.9
                    }
                ],
                "estimatedShippingCharges": [
                    {
                        "type": "SHIP_TO_HOME",
                        "charge": 8
                    },
                    {
                        "type": "SHIP_TO_STORE",
                        "charge": 0
                    }
                ],
                "items": [
                    {
                        "id": "ci11739009654",
                        "productNumber": "FC513-1507D",
                        "productUrl": "http://api.jcpenney.com/v2/products/5131507",
                        "name": " St. John's Bay?Flannel Shirt",
                        "imageUrl": "https://zoom.jcpenney.com/is/image/DP0729201318152867C.tif",
                        "activePrice": 14.99,
                        "originalPrice": 30,
                        "sale": true,
                        "savings": 15.01,
                        "quantity": 2,
                        "totalWithoutDiscount": 29.98,
                        "adjustmentsTotal": 4.5,
                        "adjustments": [
                            {
                                "type": "COUPON",
                                "code": "SHOPDEC",
                                "amount": 4.5
                            }
                        ],
                        "total": 25.48,
                        "inventoryStatus": "INSTOCK",
                        "attributes": [
                            {
                                "type": "size",
                                "value": "Medium"
                            },
                            {
                                "type": "color",
                                "value": "Charcoal"
                            }
                        ]
                    },
                    {
                        "id": "ci11739009653",
                        "productNumber": "FC251-1201D",
                        "productUrl": "http://api.jcpenney.com/v2/products/2511201",
                        "name": " Liz Claiborne Ponte Sheath Dress",
                        "imageUrl": "https://zoom.jcpenney.com/is/image/DP1003201318301485C.tif",
                        "activePrice": 35.99,
                        "originalPrice": 60,
                        "sale": true,
                        "savings": 24.01,
                        "quantity": 1,
                        "totalWithoutDiscount": 35.99,
                        "adjustmentsTotal": 5.4,
                        "adjustments": [
                            {
                                "type": "COUPON",
                                "code": "SHOPDEC",
                                "amount": 5.4
                            }
                        ],
                        "total": 35.99,
                        "inventoryStatus": "INSTOCK",
                        "attributes": [
                            {
                                "type": "size",
                                "value": "8"
                            },
                            {
                                "type": "color",
                                "value": "Black"
                            }
                        ]
                    }
                ],
                "shipping": {
                    "addressId": "addr13212354",
                    "firstName": "Alice",
                    "lastName": "Sampleton",
                    "addressLine1": "5555 Mulholland Drive",
                    "city": "Los Angeles",
                    "state": "CA",
                    "country": "US",
                    "zip": "90068",
                    "phoneNumber": "8185551234",
                    "store": false
                },
                "shippingOption": {
                    "type": "STANDARD",
                    "charge": 8,
                    "duration": "4-7 business days",
                    "selected": true
                },
                "paymentMethods": [
                    {
                        "type": "MASTERCARD",
                        "last4": "9999",
                        "expiryYear": 2014,
                        "expiryMonth": 1,
                        "address": {
                            "addressId": "addr13212354",
                            "firstName": "Alice",
                            "lastName": "Sampleton",
                            "addressLine1": "5555 Mulholland Drive",
                            "city": "Los Angeles",
                            "state": "CA",
                            "zip": "90068",
                            "country": "US",
                            "phone": "8185551234"
                        }
                    }
                ]
            }


    + Schema


            {
                    "$schema": "http://json-schema.org/draft-04/schema#",
                    "title": "Shopping bag",
                    "type": "object",
                    "properties": {
                        "email": {
                            "type": "string",
                            "description": "email address for the bag."
                        },
                        "count": {
                            "type": "integer",
                            "description": "count of products/items in the bag",
                            "default": 2
                        },
                        "total": {
                            "type": "double",
                            "description": "order total",
                            "default": 0
                        },
                        "roundUp": {
                            "type": "boolean",
                            "description": "Indicates whether the order total is to be rounded up to the nearest dollar for jcp cares charity.",
                            "default": "false"
                        },
                        "roundUpAmount": {
                            "type": "double",
                            "description": "Amount rounded up for charity from order total.",
                            "default": 0
                        },
                        "itemSubTotal": {
                            "type": "double",
                            "description": "Item subtotal or merchandise subtotal for the order.",
                            "default": 0
                        },
                        "giftWrapCharge": {
                            "type": "double",
                            "description": "Amount charged for gift wrapping the items.",
                            "default": 0
                        },
                        "adjustmentsTotal": {
                            "type": "double",
                            "description": "Sum of adjustments for the order based on promotions/reward certificates applied to the order.",
                            "default": 0
                        },
                        "adjustments": {
                            "type": "array",
                            "title": "List of adjustments for the item",
                            "items": {
                                "type": "object",
                                "title": "adjustment",
                                "properties": {
                                    "type": {
                                        "type": "string",
                                        "description": "type of adjustment",
                                        "enum": [
                                            "COUPON",
                                            "REWARDS"
                                        ]
                                    },
                                    "code": {
                                        "type": "string",
                                        "description": "Promotion code/ rewards certificate code"
                                    },
                                    "amount": {
                                        "type": "double",
                                        "description": "Reward/promo amount adjusted.",
                                        "default": 0
                                    },
                                    "serialNumber": {
                                        "type": "string",
                                        "description": "Serial number for reward certificate."
                                    }
                                },
                                "required": [
                                    "type",
                                    "code",
                                    "amount"
                                ]
                            }
                        },
                        "tax": {
                            "type": "double",
                            "description": "tax on order. Because JCPenney does business in all 50 states, we are required by law to collect all state and local sales taxes, whether the sale was made in on jcp.com, in-store or by phone.",
                            "default": 0
                        },
                        "estimatedShippingCharges": {
                            "type": "array",
                            "title": "list of shipping charges applicable to order.",
                            "items": {
                                "title": "shipping option",
                                "type": "object",
                                "properties": {
                                    "type": {
                                        "type": "string",
                                        "description": "Type of shipping charge",
                                        "enum": [
                                            "SHIP_TO_HOME",
                                            "SHIP_TO_STORE",
                                            "SHIPPING_AND_HANDLING"
                                        ]
                                    },
                                    "charge": {
                                        "type": "double",
                                        "description": "Shipping charge for the shipping option.",
                                        "default": 0
                                    }
                                },
                                "required": [
                                    "type",
                                    "charge"
                                ]
                            }
                        },
                        "subTotal": {
                            "type": "double",
                            "description": "order sub-total . i.e., itemSubtotal - adjustmentsTotal",
                            "default": 0
                        },
                        "shipping": {
                            "title": "Shipping address on order",
                            "type": "object",
                            "properties": {
                                "id": {
                                    "type": "string",
                                    "description": "Unique identifier for the address record in the application."
                                },
                                "firstName": {
                                    "type": "string",
                                    "description": "First name for the customer address.",
                                    "minLength": 1,
                                    "maxLength": 17
                                },
                                "middleInitial": {
                                    "type": "string",
                                    "description": "Middle initial for the customer address.",
                                    "minLength": 1,
                                    "maxLength": 1
                                },
                                "lastName": {
                                    "type": "string",
                                    "description": "Last name for the customer address.",
                                    "minLength": 1,
                                    "maxLength": 24
                                },
                                "company": {
                                    "type": "string",
                                    "description": "Company name for the customer address.",
                                    "minLength": 1,
                                    "maxLength": 23
                                },
                                "addressLine1": {
                                    "type": "string",
                                    "description": "Street address line 1.",
                                    "minLength": 1,
                                    "maxLength": 40
                                },
                                "addressLine2": {
                                    "type": "string",
                                    "description": "Street address line 2.",
                                    "minLength": 0,
                                    "maxLength": 40
                                },
                                "addressLine3": {
                                    "type": "string",
                                    "description": "Street address line 3. Applicable for international address only.",
                                    "minLength": 0,
                                    "maxLength": 40
                                },
                                "city": {
                                    "type": "string",
                                    "description": "City name.",
                                    "minLength": 1,
                                    "maxLength": 20
                                },
                                "APO_FPO_DPO": {
                                    "type": "string",
                                    "description": "Indicates the type of Military address",
                                    "enum": [
                                        "APO",
                                        "FPO",
                                        "DPO"
                                    ]
                                },
                                "state": {
                                    "type": "string",
                                    "description": "State code/abbreviation for US.",
                                    "maxLength": 2
                                },
                                "province": {
                                    "type": "string",
                                    "description": "Province/Territory/Region. Province code for Canada address.",
                                    "maxLength": 10
                                },
                                "zip": {
                                    "type": "string",
                                    "description": "zip code.",
                                    "maxLength": 8
                                },
                                "country": {
                                    "type": "string",
                                    "description": "Country code."
                                },
                                "phone": {
                                    "type": "string",
                                    "description": "Unformatted 10 digit phone number",
                                    "maxLength": 10
                                },
                                "secondaryPhoneNumber": {
                                    "type": "string",
                                    "description": "Unformatted 10 digit phone number. Applicable to international address only."
                                },
                                "store": {
                                    "type": "boolean",
                                    "description": "indicates whether the address is a store address",
                                    "default": false
                                },
                                "storeNumber": {
                                    "type": "string",
                                    "description": "JCPenney store number unique identifier."
                                }
                            },
                            "required": [
                                "country",
                                "firstName",
                                "lastName",
                                "addressLine1",
                                "city",
                                "state",
                                "zip",
                                "phone"
                            ]
                        },
                        "shippingOption": {
                            "type": "array",
                            "title": "The selected shipping options for the order.",
                            "items": {
                                "type": "object",
                                "title": "shipping option",
                                "properties": {
                                    "type": {
                                        "type": "string",
                                        "description": "Type of shipping option"
                                    },
                                    "charge": {
                                        "type": "double",
                                        "description": "shipping option charge",
                                        "default": 0
                                    },
                                    "duration": {
                                        "type": "string",
                                        "description": "shipping duration"
                                    },
                                    "selected": {
                                        "type": "boolean",
                                        "description": "Indicates whether the shipping option has been selected by the customer.",
                                        "default": false
                                    }
                                },
                                "required": [
                                    "type",
                                    "charge",
                                    "duration",
                                    "selected"
                                ]
                            }
                        },
                        "paymentMethods": {
                            "title": "List of payment methods ",
                            "type": "array",
                            "items": {
                                "type": "object",
                                "title": "Payment option",
                                "properties": {
                                    "type": {
                                        "type": "string",
                                        "description": "Type of card",
                                        "enum": [
                                            "MASTERCARD",
                                            "Visa",
                                            "AMEX",
                                            "DISCOVER",
                                            "JCP"
                                        ]
                                    },
                                    "last4": {
                                        "type": "string",
                                        "description": "Last 4 characters of a card. In case of JCP cards characters 6-10 of the card number.",
                                        "minLength": 4,
                                        "maxLength": 4
                                    },
                                    "expiryMonth": {
                                        "type": "integer",
                                        "description": "Expiry month of the card.",
                                        "minimum": 1,
                                        "maximum": 12
                                    },
                                    "expiryYear": {
                                        "type": "integer",
                                        "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date."
                                    },
                                    "default": {
                                        "type": "boolean",
                                        "description": "Indicates whether the card is the default payment method for the customer account.",
                                        "default": false
                                    },
                                    "address": {
                                        "title": "Address",
                                        "type": "object",
                                        "properties": {
                                            "id": {
                                                "type": "string",
                                                "description": "Unique identifier for the address record in the application."
                                            },
                                            "firstName": {
                                                "type": "string",
                                                "description": "First name for the customer address.",
                                                "minLength": 1,
                                                "maxLength": 17
                                            },
                                            "middleInitial": {
                                                "type": "string",
                                                "description": "Middle initial for the customer address.",
                                                "minLength": 1,
                                                "maxLength": 1
                                            },
                                            "lastName": {
                                                "type": "string",
                                                "description": "Last name for the customer address.",
                                                "minLength": 1,
                                                "maxLength": 24
                                            },
                                            "company": {
                                                "type": "string",
                                                "description": "Company name for the customer address.",
                                                "minLength": 1,
                                                "maxLength": 23
                                            },
                                            "addressLine1": {
                                                "type": "string",
                                                "description": "Street address line 1.",
                                                "minLength": 1,
                                                "maxLength": 40
                                            },
                                            "addressLine2": {
                                                "type": "string",
                                                "description": "Street address line 2.",
                                                "minLength": 0,
                                                "maxLength": 40
                                            },
                                            "addressLine3": {
                                                "type": "string",
                                                "description": "Street address line 3. Applicable for international address only.",
                                                "minLength": 0,
                                                "maxLength": 40
                                            },
                                            "city": {
                                                "type": "string",
                                                "description": "City name.",
                                                "minLength": 1,
                                                "maxLength": 20
                                            },
                                            "APO_FPO_DPO": {
                                                "type": "string",
                                                "description": "Indicates the type of Military address",
                                                "enum": [
                                                    "APO",
                                                    "FPO",
                                                    "DPO"
                                                ]
                                            },
                                            "state": {
                                                "type": "string",
                                                "description": "State code/abbreviation for US.",
                                                "maxLength": 2
                                            },
                                            "province": {
                                                "type": "string",
                                                "description": "Province/Territory/Region. Province code for Canada address.",
                                                "maxLength": 10
                                            },
                                            "zip": {
                                                "type": "string",
                                                "description": "zip code.",
                                                "maxLength": 8
                                            },
                                            "country": {
                                                "type": "string",
                                                "description": "Country code."
                                            },
                                            "phone": {
                                                "type": "string",
                                                "description": "Unformatted 10 digit phone number",
                                                "maxLength": 10
                                            },
                                            "secondaryPhoneNumber": {
                                                "type": "string",
                                                "description": "Unformatted 10 digit phone number. Applicable to international address only."
                                            }
                                        },
                                        "required": [
                                            "country",
                                            "firstName",
                                            "lastName",
                                            "addressLine1",
                                            "city",
                                            "state",
                                            "zip",
                                            "phone"
                                        ]
                                    }
                                },
                                "required": [
                                    "id",
                                    "type",
                                    "last4",
                                    "default",
                                    "address"
                                ]
                            }
                        },
                        "items": {
                            "type": "array",
                            "title": "list of items in bag",
                            "items": {
                                "title": "Item",
                                "type": "object",
                                "properties": {
                                    "id": {
                                        "type": "string",
                                        "description": "unique identifier for the item in the bag."
                                    },
                                    "productNumber": {
                                        "type": "string",
                                        "description": "Formatted product number."
                                    },
                                    "productUrl": {
                                        "type": "URL",
                                        "description": "URL to the catalog service to retrieve product details."
                                    },
                                    "productId": {
                                        "type": "string",
                                        "description": "11-digit SKU id for the item."
                                    },
                                    "name": {
                                        "type": "string",
                                        "description": "Name of the product."
                                    },
                                    "imageUrl": {
                                        "type": "string",
                                        "description": "URL to the image assigned to the product."
                                    },
                                    "activePrice": {
                                        "type": "double",
                                        "description": "active/current price for the product.",
                                        "default": 0
                                    },
                                    "originalPrice": {
                                        "type": "double",
                                        "description": "original price for the product.",
                                        "double": 0
                                    },
                                    "sale": {
                                        "type": "boolean",
                                        "description": "Indicates that the product is available on clearance.",
                                        "default": false
                                    },
                                    "savings": {
                                        "type": "double",
                                        "description": "Savings on the item.",
                                        "default": 0
                                    },
                                    "quantity": {
                                        "type": "integer",
                                        "description": "Number of items added to the bag",
                                        "default": 1
                                    },
                                    "totalWithoutDiscount": {
                                        "type": "double",
                                        "description": "Item total without discounts or adjustments.",
                                        "default": 0
                                    },
                                    "adjustmentsTotal": {
                                        "type": "double",
                                        "description": "Adjustments total for the item.",
                                        "default": 0
                                    },
                                    "adjustments": {
                                        "type": "array",
                                        "title": "List of adjustments for the item",
                                        "items": {
                                            "type": "object",
                                            "title": "adjustment",
                                            "properties": {
                                                "type": {
                                                    "type": "string",
                                                    "description": "type of adjustment",
                                                    "enum": [
                                                        "COUPON",
                                                        "REWARDS"
                                                    ]
                                                },
                                                "code": {
                                                    "type": "string",
                                                    "description": "Promotion code/ rewards certificate code"
                                                },
                                                "amount": {
                                                    "type": "double",
                                                    "description": "Reward/promo amount adjusted.",
                                                    "default": 0
                                                },
                                                "serialNumber": {
                                                    "type": "string",
                                                    "description": "Serial number for reward certificate."
                                                }
                                            },
                                            "required": [
                                                "type",
                                                "code",
                                                "amount"
                                            ]
                                        }
                                    },
                                    "total": {
                                        "type": "double",
                                        "description": "item total.",
                                        "default": 0
                                    },
                                    "inventoryStatus": {
                                        "type": "string",
                                        "description": "Inventory status of the item."
                                    },
                                    "attributes": {
                                        "type": "array",
                                        "title": "List of attributes for the item",
                                        "items": {
                                            "title": "Attribute",
                                            "type": "object",
                                            "properties": {
                                                "type": {
                                                    "type": "string",
                                                    "description": "Type of attribute"
                                                },
                                                "value": {
                                                    "type": "string",
                                                    "description": "value of the attribute."
                                                }
                                            },
                                            "required": [
                                                "type",
                                                "value"
                                            ]
                                        }
                                    },
                                    "parentId": {
                                        "type": "string",
                                        "description": "id of the parent item in the bag. Applicable to items with service agreements only."
                                    }
                                },
                                "required": [
                                    "id",
                                    "name",
                                    "activePrice",
                                    "originalPrice",
                                    "sale",
                                    "inventoryStatus",
                                    "description",
                                    "quantity",
                                    "productNumber",
                                    "productId",
                                    "savings",
                                    "totalWithoutDiscount",
                                    "adjustmentsTotal",
                                    "total"
                                ]
                            }
                        },
                        "giftWraps": {
                            "type": "array",
                            "title": "list of gift wraps for items in bag",
                            "items": {
                                "title": "gift wrap",
                                "type": "object",
                                "properties": {
                                    "itemIds": {
                                        "type": "array",
                                        "title": "list of items to be gift wrapped.",
                                        "items": {
                                            "title": "item id",
                                            "type": "string"
                                        }
                                    },
                                    "to": {
                                        "type": "string",
                                        "description": "gift recipient details."
                                    },
                                    "from": {
                                        "type": "string",
                                        "description": "gifter details"
                                    },
                                    "personalizedMessage": {
                                        "type": "string",
                                        "description": "personalized message for the gift wrap."
                                    },
                                    "giftWrapType": {
                                        "type": "string",
                                        "description": "type of gift wrap."
                                    }
                                },
                                "required": [
                                    "itemIds",
                                    "giftWrapType"
                                ]
                            }
                        }
                    },
                    "required": [
                        "count",
                        "total",
                        "roundUp",
                        "roundUpAmount",
                        "itemSubTotal",
                        "giftWrapCharge",
                        "adjustmentsTotal",
                        "tax",
                        "shippingCharges",
                        "subTotal",
                        "shipping"
                    ]
            }



+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body


            {
                    "errorCode": "SRV_SESSION_INVALID",
                    "errorMessage": "The customer session is invalid."
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
                    "required": ["errorCode", "errorMessage"]
                   }



+ Response 500

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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




### Place Order [POST]
This will place/complete the order in the session and a unique Order Number will be generated.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 201

    + Headers


            Content-Type: application/json
            Location: (required,URL,'https://api.jcpenney.com/v2/orders/{orderId}')


    + Body

            {

            }
    + Schema

            {

            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_ORDER_PAYMENTISNULL",
                "errorMessage": "Payment information is not provided."
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



+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_SESSION_INVALID",
                "errorMessage": "The customer's session is invalid."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

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



## Order History [/orders]
### Get Orders for Registered Customer [GET]
Retrieves all the orders present in a Registered Customer profile. This is used for Order Tracking and its response returns the status as In-process, Cancelled or Completed.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200

    + HeadersContent-Type: application/json
            X-Data-Type: String... (required, String, `OrderHistory`)

    + Body


            [
                        {
                            "number": "2013-1115-4000-6232",
                            "url": "https://api.jcpenney.com/v2/orders/2013-1115-4000-6232",
                            "orderDate": "04/21/2013",
                            "status": "CANCELLED"
                        },
                        {
                            "number": "2013-0975-4007-3811",
                            "url": "https://api.jcpenney.com/v2/orders/2013-0975-4007-3811",
                            "orderDate": "04/07/2013",
                            "status": "COMPLETED"
                        },
                        {
                            "number": "2012-2045-1007-8439",
                            "url": "https://api.jcpenney.com/v2/orders/2012-2045-1007-8439",
                            "orderDate": "07/22/2012",
                            "status": "INPROCESS"
                        }
            ]


    + Schema



                    {
                        "$schema": "http://json-schema.org/draft-04/schema#",
                        "title": "List of orders",
                        "type": "array",
                        "items": {
                            "title": "order",
                            "type": "object",
                            "properties": {
                                "number": {
                                    "type": "string",
                                    "description": "order number"
                                },
                                "url": {
                                    "type": "URL",
                                    "description": "URL to retrieve the order details"
                                },
                                "orderDate": {
                                    "type": "string",
                                    "description": "Formatted order submission date."
                                },
                                "status": {
                                    "type": "string",
                                    "description": "order status",
                                    "enum": [
                                        "INPROCESS",
                                        "CANCELLED",
                                        "COMPLETED"
                                    ]
                                }
                            },
                            "required": [
                                    "number",
                                    "url",
                                    "orderDate",
                                    "status"
                            ]
                        }





+ Response 401


    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                    "errorCode": "SRV_SESSION_INVALID",
                    "errorMessage": "The customer session is invalid."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

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






## Track Order by ID [/orders/{orderId}]
### Get Order for Registered Customer [GET]
Retrieves a particular order from a customer profile. The Order Confirmation number is provided as Input and complete order details are returned.
##### HTTPS required
##### Authentication required

+ Parameters
    + orderId (required, string, `2012-0975-8505-9577`) ... Order ID `orderId` of the submitted order to retrieve all its details.

+ Request

    + Headers

            Cookie: (required, String, `DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;DPOrder=L121950004;`)

+ Response 200
    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `Order`)
    + Body

            {
             "orderNumber": "2013-3396-2002-9978",
             "orderDate": "12/05/2013",
             "shippingStatus": "In Process",
             "shippingCarrier": "USPS",
             "shippingMethod": "HOME DELIVERY",
            "itemSubTotal": 41.99,
             "totalSavings": 0,
            "orderSubtotal": 41.99,
            "shippingAndHandling": 8,
            "tax": 4.12,
            "total": 54.11,
            "items": [
            {
            "productNumber": "FC2191238",
            "productName": "BB LS EMB NCK W/CUTO IVORY/BLK 6",
            "inventoryStatus": "INSTOCK",
            "totalWithOutDiscount": 41.99,
            "total": "41.99",
            "messages": [
                {
                    "type": "SHIPPING",
                    "data": "These items will arrive in 4 to 7 business days."
                }
            ]
             }
             ],
            "shipping": {
            "firstName": "Alice",
            "lastName": "Sampleton",
            "addressLine1": "5555 Mulholland Drive",
            "city": "Los Angeles",
            "state": "CA",
            "zip": "90068",
            "country": "US",
            "phone": "8185551234"
            },
            "paymentMethods": [
            {
            "type": "MASTERCARD",
            "last4": "9999",
            "expiryYear": 2014,
            "expiryMonth": 1,
            "address": {
                "firstName": "Alice",
                "lastName": "Sampleton",
                "addressLine1": "5555 Mulholland Drive",
                "city": "Los Angeles",
                "state": "CA",
                "zip": "90068",
                "country": "US",
                "phone": "8185551234"
            }
            }
            ]
            }



    + Schema



            {
            "$schema": "http://json-schema.org/draft-04/schema#",
            "title": "Shopping bag.",
            "type": "object",
            "properties": {
                "email": {
            "type": "string",
            "description": "email address for the bag."
                     },
                 "count": {
                  "type": "integer",
            "description": "count of products/items in the bag",
            "default": 2
              },
              "total": {
            "type": "double",
            "description": "order total",
            "default": 0
             },
             "roundUp": {
            "type": "boolean",
            "description": "Indicates whether the order total is to be rounded up to the nearest dollar for jcp cares charity.",
            "default": "false"
              },
              "roundUpAmount": {
            "type": "double",
            "description": "Amount rounded up for charity from order total.",
            "default": 0
             },
             "itemSubTotal": {
            "type": "double",
            "description": "Item subtotal or merchandise subtotal for the order.",
            "default": 0
             },
            "giftWrapCharge": {
            "type": "double",
            "description": "Amount charged for gift wrapping the items.",
            "default": 0
              },
              "adjustmentsTotal": {
            "type": "double",
            "description": "Sum of adjustments for the order based on promotions/reward certificates applied to the order.",
            "default": 0
             },
            "adjustments": {
            "type": "array",
            "title": "List of adjustments for the item",
            "items": {
                "type": "object",
                "title": "adjustment",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "type of adjustment",
                        "enum": [
                            "COUPON",
                            "REWARDS"
                        ]
                    },
                    "code": {
                        "type": "string",
                        "description": "Promotion code/ rewards certificate code"
                    },
                    "amount": {
                        "type": "double",
                        "description": "Reward/promo amount adjusted.",
                        "default": 0
                    },
                    "serialNumber": {
                        "type": "string",
                        "description": "Serial number for reward certificate."
                    }
                },
                "required": [
                    "type",
                    "code",
                    "amount"
                ]
            }
               },
            "tax": {
            "type": "double",
            "description": "tax on order. Because JCPenney does business in all 50 states, we are required by law to collect all state and local sales taxes, whether the sale was made in on jcp.com, in-store or by phone.",
            "default": 0
              },
             "shippingCharges": {
            "type": "array",
            "title": "list of shipping charges applicable to order.",
            "items": {
                "title": "shipping option",
                "type": "object",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of shipping charge",
                        "enum": [
                            "SHIP_TO_HOME",
                            "SHIP_TO_STORE",
                            "SHIPPING_AND_HANDLING"
                        ]
                    },
                    "charge": {
                        "type": "double",
                        "description": "Shipping charge for the shipping option.",
                        "default": 0
                    }
                },
                "required": [
                    "type",
                    "charge"
                ]
            }
              },
             "subTotal": {
            "type": "double",
            "description": "order sub-total . i.e., itemSubtotal - adjustmentsTotal",
            "default": 0
              },
              "shipping": {
              "title": "Shipping address on order",
               "type": "object",
               "properties": {
                "id": {
                    "type": "string",
                    "description": "Unique identifier for the address record in the application."
                },
                "firstName": {
                    "type": "string",
                    "description": "First name for the customer address.",
                    "minLength": 1,
                    "maxLength": 17
                },
                "middleInitial": {
                    "type": "string",
                    "description": "Middle initial for the customer address.",
                    "minLength": 1,
                    "maxLength": 1
                },
                "lastName": {
                    "type": "string",
                    "description": "Last name for the customer address.",
                    "minLength": 1,
                    "maxLength": 24
                },
                "company": {
                    "type": "string",
                    "description": "Company name for the customer address.",
                    "minLength": 1,
                    "maxLength": 23
                },
                "addressLine1": {
                    "type": "string",
                    "description": "Street address line 1.",
                    "minLength": 1,
                    "maxLength": 40
                },
                "addressLine2": {
                    "type": "string",
                    "description": "Street address line 2.",
                    "minLength": 0,
                    "maxLength": 40
                },
                "addressLine3": {
                    "type": "string",
                    "description": "Street address line 3. Applicable for international address only.",
                    "minLength": 0,
                    "maxLength": 40
                },
                "city": {
                    "type": "string",
                    "description": "City name.",
                    "minLength": 1,
                    "maxLength": 20
                },
                "APO_FPO_DPO": {
                    "type": "string",
                    "description": "Indicates the type of Military address",
                    "enum": [
                        "APO",
                        "FPO",
                        "DPO"
                    ]
                },
                "state": {
                    "type": "string",
                    "description": "State code/abbreviation for US.",
                    "maxLength": 2
                },
                "province": {
                    "type": "string",
                    "description": "Province/Territory/Region. Province code for Canada address.",
                    "maxLength": 10
                },
                "zip": {
                    "type": "string",
                    "description": "zip code.",
                    "maxLength": 8
                },
                "country": {
                    "type": "string",
                    "description": "Country code."
                },
                "phone": {
                    "type": "string",
                    "description": "Unformatted 10 digit phone number",
                    "maxLength": 10
                },
                "secondaryPhoneNumber": {
                    "type": "string",
                    "description": "Unformatted 10 digit phone number. Applicable to international address only."
                }
            },
            "required": [
                "country",
                "firstName",
                "lastName",
                "addressLine1",
                "city",
                "state",
                "zip",
                "phone"
            ]
             },
            "shippingOptions": {
            "type": "array",
            "title": "List of shipping options for the order.",
            "items": {
                "type": "object",
                "title": "shipping option",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of shipping option"
                    },
                    "charge": {
                        "type": "double",
                        "description": "shipping option charge",
                        "default": 0
                    },
                    "duration": {
                        "type": "string",
                        "description": "shipping duration"
                    }
                },
                "required": [
                    "type",
                    "charge",
                    "duration"
                ]
            }
             },
             "paymentMethods": {
            "title": "List of payment methods ",
            "type": "array",
            "items": {
                "type": "object",
                "title": "Payment option",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of card",
                        "enum": [
                            "MASTERCARD",
                            "Visa",
                            "AMEX",
                            "DISCOVER",
                            "JCP"
                        ]
                    },
                    "last4": {
                        "type": "string",
                        "description": "Last 4 characters of a card. In case of JCP cards characters 6-10 of the card number.",
                        "minLength": 4,
                        "maxLength": 4
                    },
                    "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month of the card.",
                        "minimum": 1,
                        "maximum": 12
                    },
                    "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date."
                    },
                    "default": {
                        "type": "boolean",
                        "description": "Indicates whether the card is the default payment method for the customer account.",
                        "default": false
                    },
                    "address": {
                        "title": "Address",
                        "type": "object",
                        "properties": {
                            "id": {
                                "type": "string",
                                "description": "Unique identifier for the address record in the application."
                            },
                            "firstName": {
                                "type": "string",
                                "description": "First name for the customer address.",
                                "minLength": 1,
                                "maxLength": 17
                            },
                            "middleInitial": {
                                "type": "string",
                                "description": "Middle initial for the customer address.",
                                "minLength": 1,
                                "maxLength": 1
                            },
                            "lastName": {
                                "type": "string",
                                "description": "Last name for the customer address.",
                                "minLength": 1,
                                "maxLength": 24
                            },
                            "company": {
                                "type": "string",
                                "description": "Company name for the customer address.",
                                "minLength": 1,
                                "maxLength": 23
                            },
                            "addressLine1": {
                                "type": "string",
                                "description": "Street address line 1.",
                                "minLength": 1,
                                "maxLength": 40
                            },
                            "addressLine2": {
                                "type": "string",
                                "description": "Street address line 2.",
                                "minLength": 0,
                                "maxLength": 40
                            },
                            "addressLine3": {
                                "type": "string",
                                "description": "Street address line 3. Applicable for international address only.",
                                "minLength": 0,
                                "maxLength": 40
                            },
                            "city": {
                                "type": "string",
                                "description": "City name.",
                                "minLength": 1,
                                "maxLength": 20
                            },
                            "APO_FPO_DPO": {
                                "type": "string",
                                "description": "Indicates the type of Military address",
                                "enum": [
                                    "APO",
                                    "FPO",
                                    "DPO"
                                ]
                            },
                            "state": {
                                "type": "string",
                                "description": "State code/abbreviation for US.",
                                "maxLength": 2
                            },
                            "province": {
                                "type": "string",
                                "description": "Province/Territory/Region. Province code for Canada address.",
                                "maxLength": 10
                            },
                            "zip": {
                                "type": "string",
                                "description": "zip code.",
                                "maxLength": 8
                            },
                            "country": {
                                "type": "string",
                                "description": "Country code."
                            },
                            "phone": {
                                "type": "string",
                                "description": "Unformatted 10 digit phone number",
                                "maxLength": 10
                            },
                            "secondaryPhoneNumber": {
                                "type": "string",
                                "description": "Unformatted 10 digit phone number. Applicable to international address only."
                            }
                        },
                        "required": [
                            "country",
                            "firstName",
                            "lastName",
                            "addressLine1",
                            "city",
                            "state",
                            "zip",
                            "phone"
                        ]
                    }
                },
                "required": [
                    "id",
                    "type",
                    "last4",
                    "default",
                    "address"
                ]
            }
            },
            "items": {
            "type": "array",
            "title": "list of items in bag",
            "items": {
                "title": "Item",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "unique identifier for the item in the bag."
                    },
                    "productNumber": {
                        "type": "string",
                        "description": "Formatted product number."
                    },
                    "productUrl": {
                        "type": "URL",
                        "description": "URL to the catalog service to retrieve product details."
                    },
                    "productId": {
                        "type": "string",
                        "description": "11-digit SKU id for the item."
                    },
                    "name": {
                        "type": "string",
                        "description": "Name of the product."
                    },
                    "imageUrl": {
                        "type": "string",
                        "description": "URL to the image assigned to the product."
                    },
                    "activePrice": {
                        "type": "double",
                        "description": "active/current price for the product.",
                        "default": 0
                    },
                    "originalPrice": {
                        "type": "double",
                        "description": "original price for the product.",
                        "double": 0
                    },
                    "sale": {
                        "type": "boolean",
                        "description": "Indicates that the product is available on clearance.",
                        "default": false
                    },
                    "savings": {
                        "type": "double",
                        "description": "Savings on the item.",
                        "default": 0
                    },
                    "quantity": {
                        "type": "integer",
                        "description": "Number of items added to the bag",
                        "default": 1
                    },
                    "totalWithoutDiscount": {
                        "type": "double",
                        "description": "Item total without discounts or adjustments.",
                        "default": 0
                    },
                    "adjustmentsTotal": {
                        "type": "double",
                        "description": "Adjustments total for the item.",
                        "default": 0
                    },
                    "adjustments": {
                        "type": "array",
                        "title": "List of adjustments for the item",
                        "items": {
                            "type": "object",
                            "title": "adjustment",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "type of adjustment",
                                    "enum": [
                                        "COUPON",
                                        "REWARDS"
                                    ]
                                },
                                "code": {
                                    "type": "string",
                                    "description": "Promotion code/ rewards certificate code"
                                },
                                "amount": {
                                    "type": "double",
                                    "description": "Reward/promo amount adjusted.",
                                    "default": 0
                                },
                                "serialNumber": {
                                    "type": "string",
                                    "description": "Serial number for reward certificate."
                                }
                            },
                            "required": [
                                "type",
                                "code",
                                "amount"
                            ]
                        }
                    },
                    "total": {
                        "type": "double",
                        "description": "item total.",
                        "default": 0
                    },
                    "inventoryStatus": {
                        "type": "string",
                        "description": "Inventory status of the item."
                    },
                    "attributes": {
                        "type": "array",
                        "title": "List of attributes for the item",
                        "items": {
                            "title": "Attribute",
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "Type of attribute"
                                },
                                "value": {
                                    "type": "string",
                                    "description": "value of the attribute."
                                }
                            },
                            "required": [
                                "type",
                                "value"
                            ]
                        }
                    },
                    "parentId": {
                        "type": "string",
                        "description": "id of the parent item in the bag. Applicable to items with service agreements only."
                    }
                },
                "required": [
                    "id",
                    "name",
                    "activePrice",
                    "originalPrice",
                    "sale",
                    "inventoryStatus",
                    "description",
                    "quantity",
                    "productNumber",
                    "productId",
                    "savings",
                    "totalWithoutDiscount",
                    "adjustmentsTotal",
                    "total"
                ]
            }
            },
             "giftWraps": {
            "type": "array",
            "title": "list of gift wraps for items in bag",
            "items": {
                "title": "gift wrap",
                "type": "object",
                "properties": {
                    "itemIds": {
                        "type": "array",
                        "title": "list of items to be gift wrapped.",
                        "items": {
                            "title": "item id",
                            "type": "string"
                        }
                    },
                    "to": {
                        "type": "string",
                        "description": "gift recipient details."
                    },
                    "from": {
                        "type": "string",
                        "description": "gifter details"
                    },
                    "personalizedMessage": {
                        "type": "string",
                        "description": "personalized message for the gift wrap."
                    },
                    "giftWrapType": {
                        "type": "string",
                        "description": "type of gift wrap."
                    }
                },
                "required": [
                    "itemIds",
                    "giftWrapType"
                ]
            }
              }
             },
             "required": [
             "count",
              "total",
             "roundUp",
             "roundUpAmount",
             "itemSubTotal",
             "giftWrapCharge",
             "adjustmentsTotal",
             "tax",
             "shippingCharges",
            "subTotal",
             "shipping"
             ]
            }



+ Response 401
    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)
    + Body


            {
            "errorCode": "SRV_SESSION_INVALID",
            "errorMessage": "The customer's session is invalid."
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
            X-Data-Type: (required, String, `ExceptionMessage`)
    + Body


            {
            "errorCode": "SRV_ORDER_NOTFOUND",
            "errorMessage": "Order not found."
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
            X-Data-Type: (required, String, `ExceptionMessage`)
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




### Get Order for Guest Customer [POST]
Retrieves order details for a Guest Customer based on validation of phone number provided for billing address on the order and the Order Confirmation number.

+ Parameters
    + orderId (required, string, `2012-0975-8505-9577`) ... Order ID `orderId` of the submitted order to retrieve all its details.

+ Request

    + Body


            [
                {
                "phone": "123-456-7890"
                }
            ]


    + Schema


                {
                "$schema": "http://json-schema.org/draft-04/schema#",
                 "title": "Phone number for validation.",
                "properties": {
                 "phone": {
                  "type": "string",
                 "description": "10 digit formatted phone number provided on the shipping address for the order."
                 }
                }
                }




+ Response 200
    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `Order`)
    + Body


            {
             "orderNumber": "2013-3396-2002-9978",
             "orderDate": "12/05/2013",
             "shippingStatus": "In Process",
             "shippingCarrier": "USPS",
             "shippingMethod": "HOME DELIVERY",
            "itemSubTotal": 41.99,
             "totalSavings": 0,
            "orderSubtotal": 41.99,
            "shippingAndHandling": 8,
            "tax": 4.12,
            "total": 54.11,
            "items": [
            {
            "productNumber": "FC2191238",
            "productName": "BB LS EMB NCK W/CUTO IVORY/BLK 6",
            "inventoryStatus": "INSTOCK",
            "totalWithOutDiscount": 41.99,
            "total": "41.99",
            "messages": [
                {
                    "type": "SHIPPING",
                    "data": "These items will arrive in 4 to 7 business days."
                }
            ]
             }
             ],
            "shipping": {
            "firstName": "Alice",
            "lastName": "Sampleton",
            "addressLine1": "5555 Mulholland Drive",
            "city": "Los Angeles",
            "state": "CA",
            "zip": "90068",
            "country": "US",
            "phone": "8185551234"
            },
            "paymentMethods": [
            {
            "type": "MASTERCARD",
            "last4": "9999",
            "expiryYear": 2014,
            "expiryMonth": 1,
            "address": {
                "firstName": "Alice",
                "lastName": "Sampleton",
                "addressLine1": "5555 Mulholland Drive",
                "city": "Los Angeles",
                "state": "CA",
                "zip": "90068",
                "country": "US",
                "phone": "8185551234"
            }
            }
            ]
            }




    + Schema


            Recommended Products assigned to the specific productId are successfully retrieved.
            {
            "$schema": "http://json-schema.org/draft-04/schema#",
            "title": "Shopping bag.",
            "type": "object",
            "properties": {
                "email": {
            "type": "string",
            "description": "email address for the bag."
                     },
                 "count": {
                  "type": "integer",
            "description": "count of products/items in the bag",
            "default": 2
              },
              "total": {
            "type": "double",
            "description": "order total",
            "default": 0
             },
             "roundUp": {
            "type": "boolean",
            "description": "Indicates whether the order total is to be rounded up to the nearest dollar for JCP cares charity.",
            "default": "false"
              },
              "roundUpAmount": {
            "type": "double",
            "description": "Amount rounded up for charity from order total.",
            "default": 0
             },
             "itemSubTotal": {
            "type": "double",
            "description": "Item subtotal or merchandise subtotal for the order.",
            "default": 0
             },
            "giftWrapCharge": {
            "type": "double",
            "description": "Amount charged for gift wrapping the items.",
            "default": 0
              },
              "adjustmentsTotal": {
            "type": "double",
            "description": "Sum of adjustments for the order based on promotions/reward certificates applied to the order.",
            "default": 0
             },
            "adjustments": {
            "type": "array",
            "title": "List of adjustments for the item",
            "items": {
                "type": "object",
                "title": "adjustment",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "type of adjustment",
                        "enum": [
                            "COUPON",
                            "REWARDS"
                        ]
                    },
                    "code": {
                        "type": "string",
                        "description": "Promotion code/ rewards certificate code"
                    },
                    "amount": {
                        "type": "double",
                        "description": "Reward/promo amount adjusted.",
                        "default": 0
                    },
                    "serialNumber": {
                        "type": "string",
                        "description": "Serial number for reward certificate."
                    }
                },
                "required": [
                    "type",
                    "code",
                    "amount"
                ]
            }
               },
            "tax": {
            "type": "double",
            "description": "tax on order. Because JCPenney does business in all 50 states, we are required by law to collect all state and local sales taxes, whether the sale was made in on jcp.com, in-store or by phone.",
            "default": 0
              },
             "shippingCharges": {
            "type": "array",
            "title": "list of shipping charges applicable to order.",
            "items": {
                "title": "shipping option",
                "type": "object",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of shipping charge",
                        "enum": [
                            "SHIP_TO_HOME",
                            "SHIP_TO_STORE",
                            "SHIPPING_AND_HANDLING"
                        ]
                    },
                    "charge": {
                        "type": "double",
                        "description": "Shipping charge for the shipping option.",
                        "default": 0
                    }
                },
                "required": [
                    "type",
                    "charge"
                ]
            }
              },
             "subTotal": {
            "type": "double",
            "description": "order sub-total . i.e., itemSubtotal - adjustmentsTotal",
            "default": 0
              },
              "shipping": {
              "title": "Shipping address on order",
               "type": "object",
               "properties": {
                "id": {
                    "type": "string",
                    "description": "Unique identifier for the address record in the application."
                },
                "firstName": {
                    "type": "string",
                    "description": "First name for the customer address.",
                    "minLength": 1,
                    "maxLength": 17
                },
                "middleInitial": {
                    "type": "string",
                    "description": "Middle initial for the customer address.",
                    "minLength": 1,
                    "maxLength": 1
                },
                "lastName": {
                    "type": "string",
                    "description": "Last name for the customer address.",
                    "minLength": 1,
                    "maxLength": 24
                },
                "company": {
                    "type": "string",
                    "description": "Company name for the customer address.",
                    "minLength": 1,
                    "maxLength": 23
                },
                "addressLine1": {
                    "type": "string",
                    "description": "Street address line 1.",
                    "minLength": 1,
                    "maxLength": 40
                },
                "addressLine2": {
                    "type": "string",
                    "description": "Street address line 2.",
                    "minLength": 0,
                    "maxLength": 40
                },
                "addressLine3": {
                    "type": "string",
                    "description": "Street address line 3. Applicable for international address only.",
                    "minLength": 0,
                    "maxLength": 40
                },
                "city": {
                    "type": "string",
                    "description": "City name.",
                    "minLength": 1,
                    "maxLength": 20
                },
                "APO_FPO_DPO": {
                    "type": "string",
                    "description": "Indicates the type of Military address",
                    "enum": [
                        "APO",
                        "FPO",
                        "DPO"
                    ]
                },
                "state": {
                    "type": "string",
                    "description": "State code/abbreviation for US.",
                    "maxLength": 2
                },
                "province": {
                    "type": "string",
                    "description": "Province/Territory/Region. Province code for Canada address.",
                    "maxLength": 10
                },
                "zip": {
                    "type": "string",
                    "description": "zip code.",
                    "maxLength": 8
                },
                "country": {
                    "type": "string",
                    "description": "Country code."
                },
                "phone": {
                    "type": "string",
                    "description": "Unformatted 10 digit phone number",
                    "maxLength": 10
                },
                "secondaryPhoneNumber": {
                    "type": "string",
                    "description": "Unformatted 10 digit phone number. Applicable to international address only."
                }
            },
            "required": [
                "country",
                "firstName",
                "lastName",
                "addressLine1",
                "city",
                "state",
                "zip",
                "phone"
            ]
             },
            "shippingOptions": {
            "type": "array",
            "title": "List of shipping options for the order.",
            "items": {
                "type": "object",
                "title": "shipping option",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of shipping option"
                    },
                    "charge": {
                        "type": "double",
                        "description": "shipping option charge",
                        "default": 0
                    },
                    "duration": {
                        "type": "string",
                        "description": "shipping duration"
                    }
                },
                "required": [
                    "type",
                    "charge",
                    "duration"
                ]
            }
             },
             "paymentMethods": {
            "title": "List of payment methods ",
            "type": "array",
            "items": {
                "type": "object",
                "title": "Payment option",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of card",
                        "enum": [
                            "MASTERCARD",
                            "Visa",
                            "AMEX",
                            "DISCOVER",
                            "JCP"
                        ]
                    },
                    "last4": {
                        "type": "string",
                        "description": "Last 4 characters of a card. In case of JCP cards characters 6-10 of the card number.",
                        "minLength": 4,
                        "maxLength": 4
                    },
                    "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month of the card.",
                        "minimum": 1,
                        "maximum": 12
                    },
                    "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date."
                    },
                    "default": {
                        "type": "boolean",
                        "description": "Indicates whether the card is the default payment method for the customer account.",
                        "default": false
                    },
                    "address": {
                        "title": "Address",
                        "type": "object",
                        "properties": {
                            "id": {
                                "type": "string",
                                "description": "Unique identifier for the address record in the application."
                            },
                            "firstName": {
                                "type": "string",
                                "description": "First name for the customer address.",
                                "minLength": 1,
                                "maxLength": 17
                            },
                            "middleInitial": {
                                "type": "string",
                                "description": "Middle initial for the customer address.",
                                "minLength": 1,
                                "maxLength": 1
                            },
                            "lastName": {
                                "type": "string",
                                "description": "Last name for the customer address.",
                                "minLength": 1,
                                "maxLength": 24
                            },
                            "company": {
                                "type": "string",
                                "description": "Company name for the customer address.",
                                "minLength": 1,
                                "maxLength": 23
                            },
                            "addressLine1": {
                                "type": "string",
                                "description": "Street address line 1.",
                                "minLength": 1,
                                "maxLength": 40
                            },
                            "addressLine2": {
                                "type": "string",
                                "description": "Street address line 2.",
                                "minLength": 0,
                                "maxLength": 40
                            },
                            "addressLine3": {
                                "type": "string",
                                "description": "Street address line 3. Applicable for international address only.",
                                "minLength": 0,
                                "maxLength": 40
                            },
                            "city": {
                                "type": "string",
                                "description": "City name.",
                                "minLength": 1,
                                "maxLength": 20
                            },
                            "APO_FPO_DPO": {
                                "type": "string",
                                "description": "Indicates the type of Military address",
                                "enum": [
                                    "APO",
                                    "FPO",
                                    "DPO"
                                ]
                            },
                            "state": {
                                "type": "string",
                                "description": "State code/abbreviation for US.",
                                "maxLength": 2
                            },
                            "province": {
                                "type": "string",
                                "description": "Province/Territory/Region. Province code for Canada address.",
                                "maxLength": 10
                            },
                            "zip": {
                                "type": "string",
                                "description": "zip code.",
                                "maxLength": 8
                            },
                            "country": {
                                "type": "string",
                                "description": "Country code."
                            },
                            "phone": {
                                "type": "string",
                                "description": "Unformatted 10 digit phone number",
                                "maxLength": 10
                            },
                            "secondaryPhoneNumber": {
                                "type": "string",
                                "description": "Unformatted 10 digit phone number. Applicable to international address only."
                            }
                        },
                        "required": [
                            "country",
                            "firstName",
                            "lastName",
                            "addressLine1",
                            "city",
                            "state",
                            "zip",
                            "phone"
                        ]
                    }
                },
                "required": [
                    "id",
                    "type",
                    "last4",
                    "default",
                    "address"
                ]
            }
            },
            "items": {
            "type": "array",
            "title": "list of items in bag",
            "items": {
                "title": "Item",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "unique identifier for the item in the bag."
                    },
                    "productNumber": {
                        "type": "string",
                        "description": "Formatted product number."
                    },
                    "productUrl": {
                        "type": "URL",
                        "description": "URL to the catalog service to retrieve product details."
                    },
                    "productId": {
                        "type": "string",
                        "description": "11-digit SKU id for the item."
                    },
                    "name": {
                        "type": "string",
                        "description": "Name of the product."
                    },
                    "imageUrl": {
                        "type": "string",
                        "description": "URL to the image assigned to the product."
                    },
                    "activePrice": {
                        "type": "double",
                        "description": "active/current price for the product.",
                        "default": 0
                    },
                    "originalPrice": {
                        "type": "double",
                        "description": "original price for the product.",
                        "double": 0
                    },
                    "sale": {
                        "type": "boolean",
                        "description": "Indicates that the product is available on clearance.",
                        "default": false
                    },
                    "savings": {
                        "type": "double",
                        "description": "Savings on the item.",
                        "default": 0
                    },
                    "quantity": {
                        "type": "integer",
                        "description": "Number of items added to the bag",
                        "default": 1
                    },
                    "totalWithoutDiscount": {
                        "type": "double",
                        "description": "Item total without discounts or adjustments.",
                        "default": 0
                    },
                    "adjustmentsTotal": {
                        "type": "double",
                        "description": "Adjustments total for the item.",
                        "default": 0
                    },
                    "adjustments": {
                        "type": "array",
                        "title": "List of adjustments for the item",
                        "items": {
                            "type": "object",
                            "title": "adjustment",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "type of adjustment",
                                    "enum": [
                                        "COUPON",
                                        "REWARDS"
                                    ]
                                },
                                "code": {
                                    "type": "string",
                                    "description": "Promotion code/ rewards certificate code"
                                },
                                "amount": {
                                    "type": "double",
                                    "description": "Reward/promo amount adjusted.",
                                    "default": 0
                                },
                                "serialNumber": {
                                    "type": "string",
                                    "description": "Serial number for reward certificat."
                                }
                            },
                            "required": [
                                "type",
                                "code",
                                "amount"
                            ]
                        }
                    },
                    "total": {
                        "type": "double",
                        "description": "item total.",
                        "default": 0
                    },
                    "inventoryStatus": {
                        "type": "string",
                        "description": "Inventory status of the item."
                    },
                    "attributes": {
                        "type": "array",
                        "title": "List of attributes for the item",
                        "items": {
                            "title": "Attribute",
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "Type of attribute"
                                },
                                "value": {
                                    "type": "string",
                                    "description": "value of the attribute."
                                }
                            },
                            "required": [
                                "type",
                                "value"
                            ]
                        }
                    },
                    "parentId": {
                        "type": "string",
                        "description": "id of the parent item in the bag. Applicable to items with service agreements only."
                    }
                },
                "required": [
                    "id",
                    "name",
                    "activePrice",
                    "originalPrice",
                    "sale",
                    "inventoryStatus",
                    "description",
                    "quantity",
                    "productNumber",
                    "productId",
                    "savings",
                    "totalWithoutDiscount",
                    "adjustmentsTotal",
                    "total"
                ]
            }
            },
             "giftWraps": {
            "type": "array",
            "title": "list of gift wraps for items in bag",
            "items": {
                "title": "gift wrap",
                "type": "object",
                "properties": {
                    "itemIds": {
                        "type": "array",
                        "title": "list of items to be gift wrapped.",
                        "items": {
                            "title": "item id",
                            "type": "string"
                        }
                    },
                    "to": {
                        "type": "string",
                        "description": "gift recepient details."
                    },
                    "from": {
                        "type": "string",
                        "description": "gifter details"
                    },
                    "personalizedMessage": {
                        "type": "string",
                        "description": "personalized message for the gift wrap."
                    },
                    "giftWrapType": {
                        "type": "string",
                        "description": "type of gift wrap."
                    }
                },
                "required": [
                    "itemIds",
                    "giftWrapType"
                ]
            }
              }
             },
             "required": [
             "count",
              "total",
             "roundUp",
             "roundUpAmount",
             "itemSubTotal",
             "giftWrapCharge",
             "adjustmentsTotal",
             "tax",
             "shippingCharges",
            "subTotal",
             "shipping"
             ]
            }



+ Response 401
    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, `ExceptionMessage`)
    + Body


            {
            "errorCode": "SRV_PHONENUMBER_INVALID",
            "errorMessage": "The phone number provided does not match the phone number on the order."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

    + Body



            {
            "errorCode": "SRV_ORDER_NOTFOUND",
             "errorMessage": "Order not found."
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
            X-Data-Type: (required, String, `ExceptionMessage`)

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



