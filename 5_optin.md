# Group Opt-In
This section explains how a user can subscribe for notifications from JCPenney.
A user can opt or subscribe for Email or Mobile notifications to receive promotional or personalized messages.
A valid email or mobile number is required submit the request.

## Subscribe via mobile/email [/optin]
### Opt-in [POST]
User can opt to receive promotion message or notification by providing valid email address or mobile number.
+ Request

    + Body

                Example for email optin.
                {
                    "type": "EMAIL"
                    "value": "alice@example.com"
                }

                Example for mobile optin.
                {
                    "type": "MOBILE"
                    "value": "8185551234"
                }
    + Schema

            {
                "$schema": "http://json-schema.org/draft-04/schema#",
                "title": "Optin",
                "type": "object",
                "properties": {
                    "type": {
                            "type": "string",
                            "description": "type of the optin",
                            "enum":[ MOBILE, EMAIL ]
                    },
                    "value": {
                            "value": "string",
                            "description": "value of the optin type."
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
            X-Data-Type: (required, String, 'ExceptionMessage')


    + Body


            {
                "errorCode": "SRV_OPTIN_MOBILE_VAL_ERR",
                "errorMessage": "Please provide valid mobile number"
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
                "errorCode": "SRV_GENERIC_ERR",
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
