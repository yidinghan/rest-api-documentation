# Group Account
Provides functionality for viewing and updating customer account information, and managing the default shipping address and payment method.  Also allows setting a default store and adding to favorites.

## Account [/customer]
Provides ability to manage customer account information.

### Create account [POST]
Creates a new customer account. User has to provide their first and last name, a unique email address (which should not already exist in the system), and password for a successful account creation.
##### HTTPS required

+ Request

    + Body

            {
                "email": "alice@example.com",
                "firstName": "Alice",
                "lastName": "Sampleton",
                "password": "2GAT123",
                "emailOptin": true
            }



    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Customer",
                "type": "object",
                "properties": {
                    "email": {
                    "type": "string",
                    "description": "Email address to uniquely identify a customer account at JCPenney."
                    },
                    "firstName": {
                    "type": "string",
                    "description": "First name of the customer."
                    },
                    "lastName": {
                    "type": "string",
                    "description": "Last name of the customer."
                    },
                    "password": {
                    "type": "string",
                    "description": "password for the customer account at JCPenney. Should contain 6-16 characters. Should not contain customer's first name, last name or email. Should not contain spaces or consecutive characters. Should not contain the string 'jcp'.",
                    "minLength": 6,
                    "maxLength": 16
                    },
                    "emailOptin": {
                    "type": "boolean",
                    "description": "Indicates whether the customer has opted in for JCPenney marketing emails.",
                    "isDefault": true
                    }
                },
                "required": [
                    "email",
                    "firstName",
                    "lastName",
                    "password",
                    "emailOptin"
                ]
            }

+ Response 201

    + Headers

            Content-Type: application/json
            Location: (required,URL,'https://api.jcpenney.com/v2/customer')


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
                "errorCode": "SRV_CUSTOMER_FIRSTNAMEISNULL",
                "errorMessage": "Enter First Name. First name value should not be null."
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


### Get Account [GET]
Retrieves account information for the logged-in customer.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Customer')

    + Body

            {
               "id": "C135430000",
               "firstName": "Dheeraj",
               "lastName": "Jain",
               "email": "dheerajatwork@gmail.com",
               "password": null,
               "emailOptin": true
            }


    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Customer basic information",
                "type": "object",
                "properties": {
                    "email": {
                        "type": "string",
                        "description": "Email address for the JCPenney customer account."
                    },
                    "firstName": {
                        "type": "string",
                        "description": "First name of the customer."
                    },
                    "lastName": {
                        "type": "string",
                        "description": "Last name of the customer."
                    },
                    "emailOptin": {
                        "type": "boolean",
                        "description": "Indicates whether the customer has opted in for JCPenney marketing email.",
                        "isDefault": true
                    }
                },
                "required": [
                    "email",
                    "firstName",
                    "lastName",
                    "emailOptin"
                ]
            }


+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body

            {
                "errorCode": "SRV_SESSION_INVALID",
                "erorMessage": "The customer's session is invalid"
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


## Session [/session]
Provides ability for users to manage their session.
### Sign in [POST]
This action will create a session for the customer with a valid email address and password. The email address and password provided in the request body should match the email address and password present in the application.
Both email address and password are case-sensitive.
##### HTTPS required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')


    + Body

            {
            "email": "betty@example.com",
            "password": "2GAT123"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Session authentication details",
                "type": "object",
                "properties": {
                    "email": {
                        "type": "string",
                        "description": "email address to uniquely identify a customer account in JCPenney."
                    },
                    "password": {
                        "type": "string",
                        "description": "password for a JCPenney customer account."
                    }
                }
            }




+ Response 201

    + Headers

            Content-Type: application/json
            DPSecureCookie: String ... (095ff3df01b128e1733fa0f0900f4766fa6;)

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
                "errorCode": "SRV_CUSTOMER_INPUTISNULL",
                "errorMessage": "Please enter username and password."
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body

            {
                "errorCode": "SRV_CUSTOMER_NOTFOUND",
                "errorMessage": "User Name or Password is incorrect."
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




### Sign out [DELETE]
This service logs out the user from the application. The session is also deleted if there is no user activity for more than x minutes (the session timeout is configurable).
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {

            }

    + Schema

            {

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
                "erorMessage": "The customer's session is invalid"
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




## Name [/customer/name]
### Update customer name [PUT]
A customer can update their first name, last name, or both once logged in.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                    "firstName": "Alice",
                    "lastName": "Sampleton"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Customer basic information",
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string",
                        "description": "First name of the Customer."
                    },
                    "lastName": {
                        "type": "string",
                        "description": "Last name of the customer."
                    }
                },
                "required": [
                    "firstName",
                    "lastName"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_FIRSTNAMEISNULL",
                "errorMessage": "Enter First Name. First name value should not be null."
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




## Email [/customer/email]
### Update customer email [PUT]
A customer can update the login email ID. This service is used to update the registered customer email address using PUT.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                "password": "2GAT123",
                "email": "betty@example.com"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Customer information",
                "type": "object",
                "properties": {
                    "password": {
                        "type": "string",
                        "description": "Password of the current JCPenney customer account."
                    },
                    "email": {
                        "type": "string",
                        "description": "New and unique email address for JCPenney customer account."
                    }
                },
                "required": [
                    "password",
                    "email"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_PASSWORDINVALID",
                "errorMessage": "Enter a valid current password."
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




## Password [/customer/password]
### Update password [PUT]
Used to change or reset customer's password. To reset the password email is passed in the request and email will be sent with password reset link.
If email and phone are available for a user, both need to be provided. Phone number becomes optional when customer account does not have phone.
##### HTTPS required


+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                    "email": "betty@example.com",
                    "phone": "818-555-1234",
                    "oldPassword": "2GAT123",
                    "newPassword": "2FAN321"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Customer information for modifying the customer password.",
                "type": "object",
                "properties": {
                    "email": {
                        "type": "string",
                        "description": "Email address of the JCPenney customer account."
                    },
                    "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number on the JCPenney customer account default address. Applicable only if address has been added to the customer information."
                    },
                    "oldPassword": {
                        "type": "string",
                        "description": "Current password of the JCPenney customer account."
                    },
                    "newPassword": {
                        "type": "string",
                        "description": "New password for the JCPenney customer account."
                    }
                },
                "required": [
                    "email"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_NOTFOUND",
                "erorMessage": "Password change creteria was not matched as per business rule."
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
                "erorMessage": "The customer's session is invalid"
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

## Addresses [/customer/addresses]
User can maintain multiple addresses in their account.
### Add a new address [POST]
Creates an address and adds it to the customer's account.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body

            {
                "firstName": "Alice",
                "middleInitial": "K",
                "lastName": "Sampleton",
                "addressLineOne": "5555 Mulholland Drive",
                "addressLineTwo": "",
                "city": "Los Angeles",
                "state": "CA",
                "zip": "90068",
                "country": "US",
                "phone": "8185551234"
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Address object",
                "type": "object",
                "properties": {
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
                        "description": "Name of the company.",
                        "minLength": 1,
                        "maxLenngth": 23
                    },
                    "addressLineOne": {
                        "type": "string",
                        "description": "Street address line 1",
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
                        "description": "Street address line 3. Applicable to international address only.",
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
                        "description": "Indicates the type of military address.",
                        "enum": [
                            "APO",
                            "FPO",
                            "DPO"
                        ]
                    },
                    "state": {
                        "type": "string",
                        "description": "state code/abbreviation for US",
                        "maxLength": 2
                    },
                    "province": {
                        "type": "string",
                        "description": "Province/Territory /Region. Province code for Canada address.",
                        "maxLength": 10
                    },
                    "zip": {
                        "type": "string",
                        "description": "zip code.",
                        "maxLength": 8
                    },
                    "country": {
                        "type": "string",
                        "description": "Country code"
                    },
                    "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number.",
                        "maxLength": 10
                    },
                    "secondaryPhone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number. Applicable to international address only.",
                        "maxLength": 10
                    }
                },
                "required": [
                    "firstName",
                    "lastName",
                    "addressLineOne",
                    "city",
                    "state",
                    "zip",
                    "phone"
                ]
            }

+ Response 201

    + Headers

            Content-Type: application/json
            Location: (required, URL, 'http://api.jcpenney.com/v2/customer/addresses/{addressId}')

    + Body

            {

            }

    + Schema

            {

            }

+ Response 400

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')
    + Body

            {
                "errorCode": "SRV_FIRSTNAME_ISNULL",
                "errorMessage": "Enter a valid first name"
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
            X-Data-Type: (required, String, 'ExceptionMessage')

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

### Get Address List [GET]
Retrieves all the addresses stored in the customer account.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Address[]')

    + Body

            [
                {
                    "id": "342342",
                    "firstName": "Alice",
                    "middleInitial": "K",
                    "lastName": "Sampleton",
                    "addressLineOne": "5555 Mulholland Drive",
                    "addressLineTwo": "",
                    "city": "Los Angeles",
                    "state": "CA",
                    "zip": "90068",
                    "country": "US",
                    "phone": "8185551234"
                },
                {
                    "id": "6456564",
                    "firstName": "Bob",
                    "middleInitial": "P",
                    "lastName": "Appleseed",
                    "addressLine1": "5700 Henry Cook Blvd",
                    "addressLine2": "Legacy Village",
                    "city": "Plano",
                    "state": "TX",
                    "zip": "75024",
                    "country": "US",
                    "phone": "9725554321"
                }
            ]

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of addresses",
                "type": "array",
                "items": {
                    "title": "Address",
                    "type": "object",
                    "properties": {
                        "id": {
                            "type": "string",
                            "description": "Unique identifier for an address record in application."
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
                            "description": "Province/Territory /Region. Province code for Canada address.",
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
            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

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

## Address [/customer/address/{addressId}]
Customer can manage their individual address
### Retrieve Address [GET]
Retrieving an address identified by its unique ID
##### HTTPS required
##### Authentication required

+ Parameters
    + addressId (required, String, `ad123456`) ... addressId an unique identifier to get the address.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Address')

    + Body

            {
                "firstName": "Alice",
                "middleInitial": "K",
                "lastName": "Sampleton",
                "addressLineOne": "5555 Mulholland Drive",
                "addressLineTwo": "",
                "city": "Los Angeles",
                "state": "CA",
                "zip": "90068",
                "country": "US",
                "phone": "1234567890"
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Address object",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier for address record in the application."
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
                        "description": "Name of the company.",
                        "minLength": 1,
                        "maxLenngth": 23
                    },
                    "addressLineOne": {
                        "type": "string",
                        "description": "Street address line 1",
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
                        "description": "Street address line 3. Applicable to international address only.",
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
                        "description": "Indicates the type of military address.",
                        "enum": [
                            "APO",
                            "FPO",
                            "DPO"
                        ]
                    },
                    "state": {
                        "type": "string",
                        "description": "state code/abbreviation for US",
                        "maxLength": 2
                    },
                    "province": {
                        "type": "string",
                        "description": "Province/Territory /Region. Province code for Canada address.",
                        "maxLength": 10
                    },
                    "zip": {
                        "type": "string",
                        "description": "zip code.",
                        "maxLength": 8
                    },
                    "country": {
                        "type": "string",
                        "description": "Country code"
                    },
                    "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number.",
                        "maxLength": 10
                    },
                    "secondaryPhone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number. Applicable to international address only.",
                        "maxLength": 10
                    }
                },
                "required": [
                    "firstName",
                    "lastName",
                    "addressLineOne",
                    "city",
                    "state",
                    "zip",
                    "phone"
                ]
            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_ADDRESS_NOTFOUND",
                "errorMessage": "Address not found."
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

### Update Address [PUT]
Modify an address identified by its unique ID.
##### HTTPS required
##### Authentication required

+ Parameters

    + addressId (required, String, `ad123456`) ... addressId an unique identifier to update the address.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body

            {
                "firstName": "Alice",
                "middleInitial": "K",
                "lastName": "Sampleton",
                "addressLineOne": "5555 Mulholland Drive",
                "addressLineTwo": "",
                "city": "Los Angeles",
                "state": "CA",
                "zip": "90068",
                "country": "US",
                "phone": "8185551234"
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Address object",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier for address record in the application."
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
                        "description": "Name of the company.",
                        "minLength": 1,
                        "maxLenngth": 23
                    },
                    "addressLineOne": {
                        "type": "string",
                        "description": "Street address line 1",
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
                        "description": "Street address line 3. Applicable to international address only.",
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
                        "description": "Indicates the type of military address.",
                        "enum": [
                            "APO",
                            "FPO",
                            "DPO"
                        ]
                    },
                    "state": {
                        "type": "string",
                        "description": "state code/abbreviation for US",
                        "maxLength": 2
                    },
                    "province": {
                        "type": "string",
                        "description": "Province/Territory /Region. Province code for Canada address.",
                        "maxLength": 10
                    },
                    "zip": {
                        "type": "string",
                        "description": "zip code.",
                        "maxLength": 8
                    },
                    "country": {
                        "type": "string",
                        "description": "Country code"
                    },
                    "phone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number.",
                        "maxLength": 10
                    },
                    "secondaryPhone": {
                        "type": "string",
                        "description": "Unformatted 10 digit phone number. Applicable to international address only.",
                        "maxLength": 10
                    }
                },
                "required": [
                    "firstName",
                    "lastName",
                    "addressLineOne",
                    "city",
                    "state",
                    "zip",
                    "phone"
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
            X-Data-Type: (required, String, 'ExceptionMessage')
    + Body

            {
                "errorCode": "SRV_FIRSTNAME_ISNULL",
                "errorMessage": "Enter a valid first name"
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
            X-Data-Type: (required, String, 'ExceptionMessage')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_ADDRESS_NOTFOUND",
                "errorMessage": "Address not found."
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

### Delete Address [DELETE]
Deletes an address identified by its unique ID.
##### HTTPS required
##### Authentication required

+ Parameters

    + addressId (required, String, `ad123456`) ... addressId an unique identifier to delete the address.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_ADDRESS_NOTFOUND",
                "errorMessage": "Address not found."
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

## Payment Methods [/customer/paymentMethods]
User can maintain multiple payment methods in their account.
### Add a new payment method [POST]
Creates new Payment method for the customer. It generally pertains to a Credit Card Information with card number, expiry date and CVV (wherever applicable)
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                   "type": "Visa",
                    "cardNumber": "9999999999999999",
                    "expiryMonth": 12,
                    "expiryYear": 2017,
                    "isDefault": true,
                    "addressId": "123456"
            }


    + Schema


            {

                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Credit card information",
                "type": "object",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of card/payment method.",
                        "enum": [
                            "MASTERCARD",
                            "Visa",
                            "JCP",
                            "DISCOVER",
                            "AMEX"
                        ]
                    },
                    "cardNumber": {
                        "type": "string",
                        "description": "Card number. Length of the field varies based on type of card. For MASTERCARD, VISA, AMEX, and DISCOVER the length of the field should be 14. For JCP the length of the field should be 11."
                    },
                    "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month on the card. Not applicable for JCP cards.",
                        "minimum": 1,
                        "maximum": 12
                    },
                    "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year on the card. Not applicable for JCP cards. Value should be equal or greater than current year. Combination of expiry month and expiry year should be greater than current date."
                    },
                    "cvv": {
                        "type": "string",
                        "description": "3 digit CVV number on the card. Card Verification # is a three-digit number found in the signature area on the back of your VISA or MasterCard credit card. This three-digit number is displayed after your credit card number. It is a four-digit number that appears on the front of your American Express card, to the right of your credit card number. Applicable for VISA cards only."
                    },
                    "isDefault": {
                        "type": "boolean",
                        "description": "Indicates whether the card is default payment method for the customer.",
                        "default": false
                    },
                    "addressId": {
                        "type": "string",
                        "description": "Unique identifier for an address applicable to the customer in the application. Address cannot be a store address. The address associated with the addressId is associated as the billing address for the card/payment method."
                    }
                },
                "required": [
                    "type",
                    "cardNumber",
                    "isDefault",
                    "addressId"
                ]

            }




+ Response 201

    + Headers

            Content-Type: application/json
            Location: (required, URL, 'https://api.jcpenney.com/v2/customer/paymentMethods')

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
                "errorCode": "SRV_CUSTOMER_CARDNUMBERISINVALID",
                "errorMessage": "Please provide a valid card number."
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
                "erorMessage": "The customer's session is invalid"
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




### Get Payment Methods List [GET]
Retrieves all the payment methods saved to the customer account.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'PaymentMethod[]')

    + Body

            [
                {
                    "id": "cc1234",
                    "type": "MASTERCARD",
                    "lastFour": "9999",
                    "expiryMonth": 1,
                    "expiryYear": 2017,
                    "isDefault": true,
                    "address": {
                        "id": "12345",
                        "firstName": "Alice",
                        "middleInitial": "",
                        "lastName": "Sampleton",
                        "company": "",
                        "addressLineOne": "5555 Mulholland Drive",
                        "addressLineTwo": "",
                        "city": "Los Angeles",
                        "state": "CA",
                        "zip": "90068",
                        "country": "US",
                        "phone": "8185551234"
                    }
                },
                {
                    "id": "cc4567",
                    "type": "Visa",
                    "lastFour": "8888",
                    "expiryMonth": 5,
                    "expiryYear": 2015,
                    "isDefault": false,
                    "address": {
                        "id": "12346",
                        "firstName": "Alice",
                        "middleInitial": "",
                        "lastName": "Sampleton",
                        "company": "",
                        "addressLineOne": "5555 Mulholland Drive",
                        "addressLineTwo": "",
                        "city": "Los Angeles",
                        "state": "CA",
                        "zip": "90068",
                        "country": "US",
                        "phone": "8185551234"
                    }
                }
            ]

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Set of payment methods for the JCPenney customer account.",
                "type": "array",
                "items": {
                    "title": "Payment method",
                    "type": "object",
                    "properties": {
                        "id": {
                            "type": "string",
                            "description": "Unique identifier of the payment method record in the application."
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
                            "description": "Last 4 charcters of a card. In case of JCP cards characters 6-10 of the card number.",
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
                        "isDefault": {
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
                                    "description": "Province/Territory /Region. Province code for Canada address.",
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
                        "isDefault",
                        "address"
                    ]
                }
            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

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

## Payment Method [/customer/paymentMethods/{paymentMethodId}]
Customer can manage individual payment method.
### Get Payment Method [GET]
Retrieves a particular payment method identified by its unique ID.
##### HTTPS required
##### Authentication required

+ Parameters

    + paymentMethodId (required, String, `usercc1400067`) ... paymentMethodId an unique identifier to get the payment method.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'PaymentMethod')

    + Body

            {
                "id": "1234",
                "type": "Visa",
                "lastFour": "9999",
                "expiryMonth": 12,
                "expiryYear": 2011,
                "isDefault": true,
                "address": {
                    "id": "12345",
                    "firstName": "Alice",
                    "middleInitial": "Sampleton",
                    "lastName": "G",
                    "company": "xxxx",
                    "addressLineOne": "5555 Mulholland Drive",
                    "addressLineTwo": "",
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
                "title": "Payment method",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier for the payment method record in the application."
                    },
                    "type": {
                        "type": "string",
                        "description": "type of card/payment method.",
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
                        "description": "Last 4 digits of a card. In case of JCP cards digits 6-10 of the card number.",
                        "minLength": 4,
                        "maxLength": 4
                    },
                    "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month on the card.",
                        "minimum": 1,
                        "maximum": 12
                    },
                    "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year of the card. Should be greater than the current year. Combination of expiry month and expiry year should be greater than the current date."
                    },
                    "isDefault": {
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
                                "description": "Province/Territory /Region. Province code for Canada address.",
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
                    "isDefault",
                    "address"
                ]
            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

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


### Update Payment Method [PUT]
Used to update a given payment method identified by its unique Id.
##### HTTPS required
##### Authentication required

+ Parameters

    + paymentMethodId (required, String, `usercc1400067`) ... paymentMethodId an unique identifier to modify the payment method.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                    "type": "Visa",
                    "cardNumber": "9999999999999999",
                    "expiryMonth": 12,
                    "expiryYear": 2011,
                    "isDefault": true,
                    "addressId": "1234"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Payment method",
                "type": "object",
                "properties": {
                    "type": {
                        "type": "string",
                        "description": "Type of card/payment method.",
                        "enum": [
                            "MASTERCARD",
                            "Visa",
                            "JCP",
                            "DISCOVER",
                            "AMEX"
                        ]
                    },
                    "cardNumber": {
                        "type": "string",
                        "description": "Card number. Length of the field varies based on type of card. For MASTERCARD, VISA, AMEX, and DISCOVER the length of the field should be 14. For JCP the length of the field should be 11."
                    },
                    "expiryMonth": {
                        "type": "integer",
                        "description": "Expiry month on the card. Not applicable for JCP cards.",
                        "minimum": 1,
                        "maximum": 12
                    },
                    "expiryYear": {
                        "type": "integer",
                        "description": "Expiry year on the card. Not applicable for JCP cards. Value should be equal or greater than current year. Combination of expiry month and expiry year should be greater than current date."
                    },
                    "cvv": {
                        "type": "string",
                        "description": "3 digit CVV number on the card. Card Verification # is a three-digit number found in the signature area on the back of your VISA or MasterCard credit card. This three-digit number is displayed after your credit card number. It is a four-digit number that appears on the front of your American Express card, to the right of your credit card number. Applicable for VISA cards only."
                    },
                    "isDefault": {
                        "type": "boolean",
                        "description": "Indicates whether the card is default payment method for the customer.",
                        "default": false
                    },
                    "addressId": {
                        "type": "string",
                        "description": "Unique identifier for an address applicable to the customer in the application. Address cannot be a store address. The address associated with the addressId is associated as the billing address for the card/payment method."
                    }
                },
                "required": [
                    "type",
                    "cardNumber",
                    "isDefault",
                    "addressId"
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

+ Response 400 (application/json)

    + Headers

            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                 "errorCode": "SRV_CUSTOMER_ADDRESSISNULL",
                "errorMessage": "Please provide an address for the payment method."
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

                "errorCode": "SVC_USR_ERR_SESSION_INVALID",
                "erorMessage": "User's session is invalid"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_PAYMENTMETHODNOTFOUND",
                "errorMessage": "Payment method not found for the customer"
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
                "errorMessage": "There was a problem while processing your request. Please try after some time."
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



### Delete Payment Method [DELETE]
Deletes a particular payment method identified by its unique Id.
##### HTTPS required
##### Authentication required

+ Parameter
    + paymentMethodId (required, String, `usercc1400067`) ... paymentMethod ID `paymentMethodId` to remove that payment method from the customer.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String

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
                "erorMessage": "User's session is invalid"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_CREDITCARDNOTFOUND",
                "errorMessage": "Credit card record is not available in the customer"
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
                "errorMessage": "There was a problem while processing your request. Please try after some time."
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




## Default Payment Method [/customer/paymentMethods/default]
### Set default payment method  [PUT]
Updates the Payment Method as default associated with the customer.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                    "paymentMethodId": "pm12345"
            }



    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Default payment id",
                "type": "object",
                "properties": {
                    "paymentMethodId": {
                        "type": "string",
                        "description": "Unique identifier for payment method in the system."
                    }
                },
                "required": [
                    "paymentMethodId"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_PAYMENTMETHODIDISNULL",
                "errorMessage": "Please provide a valid payment method id."
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
                "errorCode": "SVC_USR_ERR_SESSION_INVALID",
                "erorMessage": "User's session is invalid"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_PAYMENTMETHODNOTFOUND",
                "errorMessage": "Payment method not found for the customer"
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
                "errorCode": "SRV_GENERIC_ERROR"
                "errorMessage": "There was a problem while processing your request. Please try
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




## Stores [/customer/stores]
User can maintain multiple stores in their account.
### Add a store [POST]
Adds a store to the customer's account.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                        "firstName": "Alice",
                        "lastName": "Sampleton",
                        "phone": "8185551234",
                        "storeNumber": "0699"
                        "isDefault": true
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of stores",
                "type": "array",
                "items": {
                    "title": "Store",
                    "type": "object",
                    "properties": {
                        "firstName": {
                            "type": "string",
                            "description": "First name of the customer for the store address."
                        },
                        "lastName": {
                            "type": "string",
                            "description": "Last name of the customer for the store address."
                        },
                        "phone": {
                            "type": "string",
                            "description": "10 digit unformatted phone number for the customer."
                        },
                        "isDefault": {
                            "type": "boolean",
                            "description": "Indicates whether the store address is the default store address for the customer.",
                            "default": false
                        },
                        "storeNumber": {
                            "type": "string",
                            "description": "Unique identifier for the JCPenney store in the application."
                        }
                    },
                    "required": [
                        "firstName",
                        "lastName",
                        "phone",
                        "storeNumber",
                        "isDefault"
                    ]
                }




+ Response 201

    + Headers


            Content-Type: application/json
            Location: (required,URL,'https://api.jcpenney.com/v2/customer/stores/st12345')


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
                "errorCode": "SRV_CUSTOMER_FIRSTNAMEISNULL",
                "errorMessage": "Please enter a valid first name."
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
                "errorCode": "SRV_CUSTOMER_FIRSTNAMEISNULL",
                "errorMessage": "Enter First Name. First name value should not be null."
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




### Get Store List [GET]
Retrives all saved stores from the customer account.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `Stores`)
    + Body


            [
                {
                    "id": "123434",
                    "firstName": "Alice",
                    "lastName": "Sampleton",
                    "phone": "8185551234",
                    "storeNumber": "0699",
                    "addressLineOne": "Glendale Galleria",
                    "addressLineTwo": "1169 Glendale Galleria",
                    "city": "Glendale",
                    "state": "CA",
                    "zip": "91210",
                    "country": "US",
                    "storePhone": "818-240-8700",
                    "isDefault": true
                },
                {
                    "id": "23321312",
                    "firstName": "Bob",
                    "lastName": "Appleseed",
                    "phone": "1234567890",
                    "storeNumber": "67890",
                    "addressLineOne": "Stonebriar Mall",
                    "addressLineTwo": "2607 Preston Rd",
                    "city": "Frisco",
                    "state": "TX",
                    "zip": "75034",
                    "addressCountry": "US",
                    "storePhone": "972-712-2707",
                    "isDefault": false
                }
            ]


    + Schema


            {
            "$schema": "http://json-schema.org/draft-04/schema#",
            "title": "List of stores",
            "type": "array",
            "items": {
                "title": "Store",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier to store address n the application for the customer."
                    },
                    "firstName": {
                        "type": "string",
                        "description": "First name of the customer for the store address."
                    },
                    "lastName": {
                        "type": "string",
                        "description": "Last name of the customer for the store address."
                    },
                    "phone": {
                        "type": "string",
                        "description": "10 digit unformatted phone number for the customer."
                    },
                    "isDefault": {
                        "type": "boolean",
                        "description": "Indicates whether the store address is the default store address for the customer.",
                        "default": false
                    },
                    "storeNumber": {
                        "type": "string",
                        "description": "Unique identifier for the JCPenney store in the application."
                    },
                    "storePhone": {
                        "type": "string",
                        "description": "Formatted phone number for the store."
                    },
                    "addressLineOne": {
                        "type": "string",
                        "description": "Street address line 1 for the store address."
                    },
                    "addressLineTwo": {
                        "type": "string",
                        "description": "Street address line 2 for the store address."
                    },
                    "city": {
                        "type": "string",
                        "description": "city where the JCPenney store is located."
                    },
                    "state": {
                        "type": "string",
                        "description": "State where the JCPenney store is located."
                    },
                    "zip": {
                        "type": "string",
                        "description": "zip code of the location where the JCPenney store is located."
                    },
                    "country": {
                        "type": "string",
                        "description": "Store address country."
                    }
                },
                "required": [
                    "id",
                    "firstName",
                    "lastName",
                    "phone",
                    "storeNumber",
                    "addressLineOne",
                    "city",
                    "state",
                    "zip",
                    "country",
                    "storePhone",
                    "isDefault"
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




## Store [/customer/stores/{storeId}]
User can manage individual store.
### Get Store [GET]
Retrieves store details from the customer account identified by its unique Id.
##### HTTPS required
##### Authentication required

+ Parameters

    + storeId (required, String, ``st12345``) ... storeId an unique identifier.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `Stores`)

    + Body


            {
                "id": "123434",
                "firstName": "Alice",
                "lastName": "Sampleton",
                "phone": "818-555-1234",
                "storeNumber": "0699",
                "addressLineOne": "Glendale Galleria",
                "addressLineTwo": "1169 Glendale Galleria",
                "city": "Glendale",
                "state": "CA",
                "zip": "91210",
                "country": "US",
                "storePhone": "818-240-8700",
                "isDefault": true
            }



    + Schema


            {
            "$schema": "http://json-schema.org/draft-04/schema#",
            "title": "Store",
            "type": "object",
            "properties": {
                "id": {
                    "type": "string",
                    "description": "Unique identifier to store address n the application for the customer."
                },
                "firstName": {
                    "type": "string",
                    "description": "First name of the customer for the store address."
                },
                "lastName": {
                    "type": "string",
                    "description": "Last name of the customer for the store address."
                },
                "phone": {
                    "type": "string",
                    "description": "10 digit unformatted phone number for the customer."
                },
                "isDefault": {
                    "type": "boolean",
                    "description": "Indicates whether the store address is the default store address for the customer.",
                    "default": false
                },
                "storeNumber": {
                    "type": "string",
                    "description": "Unique identifier for the JCPenney store in the application."
                },
                "storePhone": {
                    "type": "string",
                    "description": "Formatted phone number for the store."
                },
                "addressLineOne": {
                    "type": "string",
                    "description": "Street address line 1 for the store address."
                },
                "addressLineTwo": {
                    "type": "string",
                    "description": "Street address line 2 for the store address."
                },
                "city": {
                    "type": "string",
                    "description": "city where the JCPenney store is located."
                },
                "state": {
                    "type": "string",
                    "description": "State where the JCPenney store is located."
                },
                "zip": {
                    "type": "string",
                    "description": "zip code of the location where the JCPenney store is located."
                },
                "country": {
                    "type": "string",
                    "description": "Store address country."
                }
            },
            "required": [
                "id",
                "firstName",
                "lastName",
                "phone",
                "storeNumber",
                "addressLineOne",
                "city",
                "state",
                "zip",
                "country",
                "storePhone",
                "isDefault"
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




+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_STORENOTFOUND",
                "errorMessage": "Store record is not available in the customer"
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




### Update Store Details [PUT]
Modify store details from the customer account identified by its unique Id.
A change may include customer First Name, Last Name or Phone number.
##### HTTPS required
##### Authentication required

+ Parameters

    + storeId (required, String, `st12345`) ... storeId an unique identifier.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                    "firstName": "Alice",
                    "lastName": "Sampleton",
                    "phone": "818-555-1234",
                    "storeNumber": "0699"
                    "isDefault": true
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Store",
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string",
                        "description": "First name of the customer for the store address."
                    },
                    "lastName": {
                        "type": "string",
                        "description": "Last name of the customer for the store address."
                    },
                    "phone": {
                        "type": "string",
                        "description": "10 digit unformatted phone number for the customer."
                    },
                    "isDefault": {
                        "type": "boolean",
                        "description": "Indicates whether the store address is the default store address for the customer.",
                        "default": false
                    },
                    "storeNumber": {
                        "type": "string",
                        "description": "Unique identifier for the JCPenney store in the application."
                    }
                },
                "required": [
                    "firstName",
                    "lastName",
                    "phone",
                    "storeNumber",
                    "isDefault"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_FIRSTNAMEISNULL",
                "errorMessage": "Please enter a valid first name."
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




+ Response 404

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_STORENOTFOUND",
                "errorMessage": "Store record is not available in the customer"
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




### Delete Store [DELETE]
Deletes a particular store from the customer account identified by its unique id.
##### HTTPS required
##### Authentication required

+ Parameters

    + storeId (required, String, `st12345`) ... storeId an unique identifier.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_STORENOTFOUND",
                "errorMessage": "Store record is not available in the customer"
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




## Default Store [/customer/stores/default]
### Set default store [PUT]
Used to update a particular store as default. It is identified by its unique Id.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body


            {
                "id": "12345"
            }


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Store",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier to identify the store address record for the customer in the application."
                    }
                },
                "required": [
                    "id"
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
            X-Data-Type: String ... (required, String, `ExceptionMessage`)

    + Body


            {
                "errorCode": "SRV_CUSTOMER_STORENOTFOUND",
                "errorMessage": "Store record is not available in the customer"
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




## Preferences [/customer/preferences]
Customer can maintain their preferences.

### Update preferences [PUT]

Updates the Customer Preferences for receiving alerts through Emails or Mobile SMS.
Alerts could be in form of promotions or reminders of Shopping Bag or Favorites.
A customer can opt-in or opt-out of these preference as per will.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')


    + Body


            [
                {
                    "name": "emailOffers",
                    "subscribed": true
                },
                {
                    "name": "mobileOffers",
                    "subscribed": true,
                    "phone": "2144367985"
                },
                {
                    "name": "shoppingBagReminder",
                    "subscribed": false
                },
                {
                    "name": "favoritesReminder",
                    "subscribed": false
                },
                {
                    "name": "surveyReminder",
                    "subscribed": false
                },
                {
                    "name": "reviewNotificationReminder",
                    "subscribed": false
                }
            ]


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of preferences.",
                "type": "array",
                "items": {
                    "title": "preference",
                    "type": "object",
                    "properties": {
                        "name": {
                            "type": "string",
                            "description": "name of the preference.",
                            "enum": [
                                "EMAILOFFERS",
                                "MOBILEOFFERS",
                                "SHOPPINGBAGREMINDERS",
                                "FAVORITESREMINDER",
                                "SURVEYPARTICIPATIONREMINDER",
                                "RATINGREVIEWNOTIFICATION",
                                "SHARECREDITHISTORYINFO",
                                "SHARECUSTOMERINFO"
                            ]
                        },
                        "subscribed": {
                            "type": "boolean",
                            "description": "indicates whether the current customer preference is selected.",
                            "default": false
                        },
                        "frequency": {
                            "type": "string",
                            "description": "Frequency for receiving JCPenney email's. Applicable to preference - EMAILOFFERS only.",
                            "enum": [
                                "ASAVAILBLE",
                                "WEEKLY",
                                "MONTHLY"
                            ]
                        },
                        "interests": {
                            "type": "array",
                            "title": "List of interests.",
                            "items": {
                                "title": "Interest",
                                "type": "string",
                                "description": "Customer interest. Applicable to preference - EMAILOFFERS only.",
                                "enum": [
                                    "MENS",
                                    "WOMEN",
                                    "CHILDREN",
                                    "HOMEOUTDOORLIVING"
                                ]
                            }
                        },
                        "phone": {
                            "type": "string",
                            "description": "Phone number for MOBILEOFFERS only"
                        }
                    },
                    "required": [
                        "name",
                        "subscribed"
                    ]
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




### Get Preferences List [GET]
Retrieve customer preferences saved in the account.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: String ... (required, String, `Preference[]`)

    + Body


            [
                {
                    "name": "emailOffers",
                    "subscribed": true
                },
                {
                    "name": "mobileOffers",
                    "subscribed": true,
                    "phone": "2144367985"
                },
                {
                    "name": "shoppingBagReminder",
                    "subscribed": false
                },
                {
                    "name": "favoritesReminder",
                    "subscribed": false
                },
                {
                    "name": "surveyReminder",
                    "subscribed": false
                },
                {
                    "name": "reviewNotificationReminder",
                    "subscribed": false
                }
            ]


    + Schema


            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of preferences.",
                "type": "array",
                "items": {
                    "title": "preference",
                    "type": "object",
                    "properties": {
                        "name": {
                            "type": "string",
                            "description": "name of the preference.",
                            "enum": [
                                "EMAILOFFERS",
                                "MOBILEOFFERS",
                                "SHOPPINGBAGREMINDERS",
                                "FAVORITESREMINDER",
                                "SURVEYPARTICIPATIONREMINDER",
                                "RATINGREVIEWNOTIFICATION",
                                "SHARECREDITHISTORYINFO",
                                "SHARECUSTOMERINFO"
                            ]
                        },
                        "subscribed": {
                            "type": "boolean",
                            "description": "indicates whether the current customer preference is selected.",
                            "default": false
                        },
                        "frequency": {
                            "type": "string",
                            "description": "Frequency for receiving JCPenney email's. Applicable to preference - EMAILOFFERS only.",
                            "enum": [
                                "ASAVAILBLE",
                                "WEEKLY",
                                "MONTHLY"
                            ]
                        },
                        "interests": {
                            "type": "array",
                            "title": "List of interests.",
                            "items": {
                                "title": "Interest",
                                "type": "string",
                                "description": "Customer interest. Applicable to preference - EMAILOFFERS only.",
                                "enum": [
                                    "MENS",
                                    "WOMEN",
                                    "CHILDREN",
                                    "HOMEOUTDOORLIVING"
                                ]
                            }
                        },
                        "phone": {
                            "type": "string",
                            "description": "Phone number for MOBILEOFFERS only"
                        }
                    },
                    "required": [
                        "name",
                        "subscribed"
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




## Favorites [/customer/favorites]
Provides the ability to manage the customer's favorites list.

### Add Favorites [POST]
Adds an item to the customer's favorites.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body

            **Request for adding a regular product to favorites.**

            {
                "items": [
                    {
                        "skuId": "22906380042",
                        "quantity": 1
                    }
                ]
            }

            **Request for adding a product with service aggreement to favorites**

            {
                "items": [
                    {
                        "skuId": "86930540018",
                        "quantity": 1
                    },
                    {
                        "skuId": "86991460000",
                        "quanatity": 1
                    }
                ]
            }

            **Request for adding a product with Variable data information (Monogram)**

            {
                "items": [
                    {
                        "skuId": "53180980315",
                        "quantity": 1,
                        "attributes": [
                            {
                                "type": "TYPE (MONO/PERSONLZ)",
                                "value": "3"
                            },
                            {
                                "type": "THREAD COLOR",
                                "value": "K"
                            },
                            {
                                "type": "POSITION / LOCATION",
                                "value": "L"
                            },
                            {
                                "type": "POSITION / LOCATION",
                                "value": "L"
                            },
                            {
                                "type": "FIRST NAME INITIAL",
                                "value": "A"
                            },
                            {
                                "type": "MIDDLE NAME INITIAL",
                                "value": "L"
                            },
                            {
                                "type": "LAST NAME INITIAL",
                                "value": "P"
                            }
                        ]
                    }
                ]
            }

    + Schema

            {
                "type": "object",
                "required": [
                    "items"
                ],
                "properties": {
                    "items": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "required": [
                                "skuId",
                                "quantity"
                            ],
                            "properties": {
                                "skuId": {
                                    "type": "string",
                                    "minLength": 13,
                                    "maxLength": 13
                                },
                                "attributes": {
                                    "type": "array",
                                    "items": {
                                        "type": "object",
                                        "$schema": "http://json-schema.org/draft-04/schema#",
                                        "description": "Represented the attributes.",
                                        "title": "Attribute",
                                        "required": [
                                            "value",
                                            "type"
                                        ],
                                        "properties": {
                                            "value": {
                                                "type": "string",
                                                "description": "value of the attribute."
                                            },
                                            "type": {
                                                "type": "string",
                                                "description": "type of attribute."
                                            }
                                        }
                                    }
                                },
                                "quantity": {
                                    "type": "integer",
                                    "maximum": 99,
                                    "minimum": 1
                                }
                            }
                        },
                        "uniqueItems": true
                    }
                }
            }

+ Response 201

    + Headers

            Location: (required, URL, 'https://api.jcpenney.com/v2/customer/favorites')

    + Body

            {

            }

    + Schema

            {

            }

+ Response 400


    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            Response when an invalid product is added to customer favorites.

            {
                "errorCode": "SRV_PRODUCT_NOTFOUND",
                "errorMessage": "Product not found."
            }

            Response when an invalid quantity is provided in the request.

            {
                "errorCode": "SRV_QUANTITY_INVALID",
                "errroMessage": "Please provide a valid quantity."
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
            X-Data-Type: (required, String, 'ExceptionMessage')

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

### Get Favorites List [GET]
Retrieve all favorites from the customer account.
##### HTTPS required
##### Authentication required

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Favorite[]')

    + Body

            [
                {
                    "id": "8691974",
                    "name": "Dyson® DC41 Animal™ Vacuum Cleaner",
                    "imageURL": "https://zoom.jcpenney.com/is/image/DP0507201318124873C.tif",
                    "activePrice": 599.99,
                    "originalPrice": 670,
                    "sale": true,
                    "inventoryMessage": "Instock",
                    "description": "Dyson® DC41 Animal™ Vacuum Cleaner",
                    "attributes": [
                        {
                            "type": "Product",
                            "value": "Dyson Dc41 Animal Upright"
                        },
                        {
                            "type": "Color",
                            "value": "Iron/satin Purple"
                        }
                    ],
                    "quantity": 2,
                    "productURL": "http://api.jcpenney.com/products/8691974",
                    "productNumber": "BG869-1974"
                },
                {
                    "id": "8699150",
                    "parentId": "8691974",
                    "name": "1YR SVS PLAN POS",
                    "activePrice": 25,
                    "originalPrice": 25,
                    "sale": true,
                    "description": "1YR SVS PLAN POS",
                    "quantity": 1,
                    "productNumber": "ES869-9150"
                }
            ]

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "List of favorite items",
                "type": "array",
                "items": {
                    "title": "Favorite item",
                    "type": "object",
                    "properties": {
                        "id": {
                            "type": "string",
                            "description": "Unique identifier for a favorite item for the customer in the application."
                        },
                        "name": {
                            "type": "string",
                            "description": "Name of the product added to favorite."
                        },
                        "imageUrl": {
                            "type": "URL",
                            "description": "URL to the image assigned to the product added to favorite."
                        },
                        "activePrice": {
                            "type": "double",
                            "description": "Current price of the product.",
                            "default": 0
                        },
                        "originalPrice": {
                            "type": "double",
                            "description": "Original price of the product.",
                            "default": 0
                        },
                        "sale": {
                            "type": "boolean",
                            "description": "Indicates whether the product is available on clearance.",
                            "default": false
                        },
                        "inventoryMessage": {
                            "type": "string",
                            "description": "Formatted string representation of the inventory for the product."
                        },
                        "description": {
                            "type": "string",
                            "description": "Descripiton of the product."
                        },
                        "attributes": {
                            "type": "array",
                            "title": "List of attributes applicable to the favorite item.",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "Type of attribute"
                                },
                                "value": {
                                    "type": "string",
                                    "description": "Value of the attribute"
                                }
                            },
                            "required": [
                                "type",
                                "value"
                            ]
                        },
                        "quantity": {
                            "type": "integer",
                            "description": "Number of items added to favorite.",
                            "default": 1
                        },
                        "productURL": {
                            "type": "URL",
                            "description": "JCPenney catalog REST API URL to the product."
                        },
                        "productNumber": {
                            "type": "string",
                            "description": "Formatted product number."
                        },
                        "productId": {
                            "type": "string",
                            "description": "11-digit SKU Id representing the product added to favorite."
                        },
                        "parentId": {
                            "type": "string",
                            "description": "parent favorite item id. Applicable only when product with service agreement is added to favorites."
                        }
                    },
                    "required": [
                        "id",
                        "name",
                        "activePrice",
                        "originalPrice",
                        "sale",
                        "inventoryMessage",
                        "description",
                        "quantity",
                        "productNumber",
                        "productId"
                    ]
                }
            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

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

## Favorite [/customer/favorites/{favoriteItemId}]
Managing an individual favorite item.
### Get Favorite [GET]
Retrieve a favorite identified by a given ID.
##### HTTPS required
##### Authentication required

+ Parameters

    + favoriteItemId (required, String, `gi12345`) ... favoriteItemId a unique identifier to get item.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

+ Response 200

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'Favorite')

    + Body

            {
                "id": "1234567",
                "name": "Arizona Cargo Pants",
                "imageURL": "https://www.jcpenney.com/dotcom/images/DP0520201317023164M.jpg",
                "activePrice": 10,
                "originalPrice": 12,
                "sale": true,
                "inventoryMessage": "Instock",
                "description": "Arizona Cargo Pants",
                "attributes": [
                    {
                        "type": "Color",
                        "value": "Dark Olive"
                    }
                ],
                "quantity": 2,
                "productURL": "http://api.jcpenney.com/products/1234567",
                "productNumber": "BG123-4567"
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Favorite item",
                "type": "object",
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Unique identifier for a favorite item for the customer in the application."
                    },
                    "name": {
                        "type": "string",
                        "description": "Name of the product added to favorite."
                    },
                    "imageUrl": {
                        "type": "URL",
                        "description": "URL to the image assigned to the product added to favorite."
                    },
                    "activePrice": {
                        "type": "double",
                        "description": "Current price of the product.",
                        "default": 0
                    },
                    "originalPrice": {
                        "type": "double",
                        "description": "Original price of the product.",
                        "default": 0
                    },
                    "sale": {
                        "type": "boolean",
                        "description": "Indicates whether the product is available on clearance.",
                        "default": "false"
                    },
                    "inventoryMessage": {
                        "type": "string",
                        "description": "Formatted inventory message for the product."
                    },
                    "description": {
                        "type": "string",
                        "description": "Description for the product in favorite."
                    },
                    "attributes": {
                        "type": "array",
                        "title": "List of attributes applicable to the favorite item.",
                        "properties": {
                            "type": {
                                "type": "string",
                                "description": "Type of attribute"
                            },
                            "value": {
                                "type": "string",
                                "description": "Value of the attribute"
                            }
                        },
                        "quantity": {
                            "type": "integer",
                            "description": "Number of items added to favorite.",
                            "default": 1
                        },
                        "productURL": {
                            "type": "URL",
                            "description": "JCPenney catalog REST API URL to the product."
                        },
                        "productNumber": {
                            "type": "string",
                            "description": "Formatted product number."
                        },
                        "productId": {
                            "type": "string",
                            "description": "11-digit SKU Id representing the product added to favorite."
                        },
                        "parentId": {
                            "type": "string",
                            "description": "parent favorite item id. Applicable only when product with service agreement is added to favorites."
                        }
                    },
                    "required": [
                        "id",
                        "name",
                        "activePrice",
                        "originalPrice",
                        "sale",
                        "inventoryMessage",
                        "description",
                        "quantity",
                        "productNumber",
                        "productId"
                    ]
                }
            }

+ Response 401

    + Headers

            Content-Type: application/json
            X-Data-Type: (required, String, 'ExceptionMessage')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_FAVORITEITEM_NOTFOUND",
                "errorMessage": "Favorite item not found."
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

### Update Favorite [PUT]
Edits the Favorite, may include changing SKUs or quantity.
##### HTTPS required
##### Authentication required

+ Parameters

    + favoriteItemId (required, String, `gi12345`) ... favoriteItemId an unique identifier to update gift item.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

    + Body

            {
                "skuId": "12345670002",
                "quantity": 1
            }

    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Favorite input item",
                "type": "object",
                "properties": {
                    "skuId": {
                        "type": "string",
                        "description": "11-digit SKU identifier for the item being added."
                    },
                    "quantity": {
                        "type": "integer",
                        "description": "Non zero, non-negative integer representing the number of items being added.",
                        "default": 1
                    },
                    "attributes": {
                        "type": "array",
                        "title": "List of attributes applicable to the favorite item.",
                        "properties": {
                            "type": {
                                "type": "string",
                                "description": "Type of attribute"
                            },
                            "value": {
                                "type": "string",
                                "description": "Value of the attribute"
                            }
                        }
                    }
                },
                "required": [
                    "skuId",
                    "quantity"
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
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            Response when an invalid product is added to customer favorites.

            {
                "errorCode": "SRV_PRODUCT_NOTFOUND",
                "errorMessage": "Product not found."
            }

            Response when an invalid quantity is provided in the request.

            {
                "errorCode": "SRV_QUANTITY_INVALID",
                "errroMessage": "Please provide a valid quantity."
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
            X-Data-Type: (required, String, 'ExceptionMessage')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_FAVORITEITEM_NOTFOUND",
                "errorMessage": "Favorite item not found."
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

### Delete Favorite [DELETE]
Deletes the favorite matching the request URL, identified by its unique id.
##### HTTPS required
##### Authentication required

+ Parameters

    + favoriteItemId (required, String, `gi12345`) ... favoriteItemId an unique identifier to delete gift item.

+ Request

    + Headers

            Cookie:(required, String, 'DPJSESSIONID=0000Q6fR2-IBW5m4u6N8iZnXOzL:16r1lv9on;DPSecureCookie=34887f898a43f791137ff3a37abaee0f;')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

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
            X-Data-Type: (required, String, 'ExceptionMessage')

    + Body

            {
                "errorCode": "SRV_FAVORITEITEM_NOTFOUND",
                "errorMessage": "Favorite item not found."
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
