FORMAT:1A
FORMAT: 1A
HOST: http://api.jcpenney.com

# Contents
1. [Layout](#Layout)
2. [Services](#Services)
3. [How to view and edit](#View)


<a name="Layout"/>
## Layout

Each file contains a documentation of list of operations about a particular resource. For example "Catalog.md" file contains documentation of the list of
operations that can be performed on catalog. Each file starts with a "FORMAT" which is used to version the documentation. Following the "FORMAT" is the 
"HOST" which describes where the services are hosted. Following the "HOST" is a "GROUP" header which tells the group under which the services are categorized.
For example ""Catalog.md" will have a Catalog "GROUP". Following the "GROUP" are sub-sections of the particular resource. For example Catalog group has 
departments, categories as it's sub-sections. The operations on sub-sections are explained in detail in the order of post, get, put and delete(which ever are 
applicable).

<a name="Services"/>
## Services

For each service the url of the service is documented. Following this is a brief description of the service. Following this are the request 
and response objects. For post and put Each operation has a request body and schema whereas for get and delete the query parameters are documented in detail. The response 
contains  headers, body and schema. Response is arranged in order of 200(get,put and delete)/201(for post), 400 , 401, 403 and 500 (where ever applicable).The
default value for request header "Content-Type" is "application/json". Along with this header there might also be other cookie headers like "DPJSessionId"
and "DPOrder". The response also has a "Content-Type" with value "application/json". Along with this it has a "X-Data-Type" header which is a String value 
of the class name of the response object.

<a name="View"/>
## How to view and edit

To view the documented Rest APIs copy the contents of the .md file to "https://app.apiary.io/{username}/editor" and click on the preview button.
Any text editor can be used to edit the contents of the .md file, however it is recommended to use the editor in the url provided above as text editors cause
formatting issues.
 
