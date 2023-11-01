# Salesforce REST API Connectivity using Boomi

## Problem Statement
There can be several teams in an organization who need to connect to a Salesforce organization to get/send data. Salesforce Architects usually recommend to have separate users for separate projects so that the various access levels and roles can be segregated from a security standpoint.

## Limitation of Native Salesforce Connector
Suppose if there are 7 separate users created for Boomi integration in a Salesforce organization, and we decide to use Boomi's native/out-of-box Salesforce Connector, it will cost 7 licenses and the operational cost of Boomi would increase.

## Benefits of using Salesforce REST API in Boomi Integrations
:small_orange_diamond: Reduced Boomi License Cost - Since a single HTTP Connector in Boomi can be used by parameterizing the credentials of different integration users.

:small_orange_diamond: Better Security - We can use OAuth 2.0 as the authentication and authorization mechanism for enhanced security.

:small_orange_diamond: Faster Connectvity - Boomi's native/out-of-box Salesforce Connector conncts with the SOAP API of Salesforce, which can be slower at times, as compared to the REST API of Salesforce.

:small_orange_diamond: Faster Integration Enhancements - When we use Boomi's native/out-of-box Salesforce Connector to perform Salesforce QUERY operation, and have to update the SOQL to incorporate a new Salesforce field, we have to re-import the Salesforce Object in the Boomi's Salesforce Connector's Operation along with verifying the selected fields to avoid any additional fields being selected after the profile re-import. When we use Boomi's HTTP Connector to perform Salesforce QUERY operation, we only have to edit the parameter in the URI.

## Solution Approach
:small_orange_diamond: Create a Connected App in Salesforce with the required configuration and access-levels.

:small_orange_diamond: Create the Main Boomi Process.

:small_orange_diamond: Create an HTTP Client Connector component and set the URL.

:small_orange_diamond: Create the required Operations for HTTP Client Connector component.

:small_orange_diamond: Create a common reusable sub-process to fetch the Salesforce Access Token.

## Create Connected App in Salesforce
Please refer this Salesforce community article - https://developer.salesforce.com/docs/atlas.en-us.196.0.api_rest.meta/api_rest/intro_defining_remote_access_applications.htm 

## Create HTTP Client Connector in Boomi
:small_orange_diamond: URL: Enter the Base-URL.
```
https://<salesforce_instance_name>.my.salesforce.com
```

:small_orange_diamond: Authentication Type: None

<img width="597" alt="image" src="https://github.com/ayanpan/sfdc-rest-api-boomi/assets/12267939/1a95a1b2-bfee-4f32-9b0f-042ee9fed3c4">

## Generate Salesforce Access Token
:small_orange_diamond: Create the payload in a Message shape, based on **application/x-www-form-urlencoded** Content-Type.
```
grant_type=password&client_id={1}&client_secret={2}&username={3}&password={4}
```
<img width="539" alt="image" src="https://github.com/ayanpan/sfdc-rest-api-boomi/assets/12267939/24ce8a79-dc30-4568-8ae2-280b2732f67a">

:small_orange_diamond: Set the HTTP Operation's Resource Path in a DDP, in the Set Properties shape.
```
DDP_Token_RPath: services/oauth2/token
```

<img width="539" alt="image" src="https://github.com/ayanpan/sfdc-rest-api-boomi/assets/12267939/86922642-b638-471a-b822-7b83230467a6">

:small_orange_diamond: Configure the HTTP Client Connector's Operation.
```
Select Request Profile Type: NONE
Select Response Profile Type:	JSON
Content Type: application/x-www-form-urlencoded
HTTP Method: POST
```
<img width="701" alt="image" src="https://github.com/ayanpan/sfdc-rest-api-boomi/assets/12267939/d5c1bed4-ee5f-4822-854f-4290e60f0a8a">

:small_orange_diamond: Store the value of Access Token in a DPP.
```
DPP_Access_Token: Bearer <value_of_access_token_recieved_from_salesforce>
```

## Salesforce QUERY Operation

## Salesforce CREATE Operation

## Salesforce UPDATE Operation

## Salesforce UPSERT Operation

## List of Abbreviations
| Abbreviation  | Definition |
| ------------- | ------------- |
| REST  | Representational State Transfer  |
| API  | Application Programming Interface  |
| HTTP  | Hypertext Transfer Protocol  |
| OAuth | open authorization  |
| SOAP  | Simple Object Access Protocol |
| URL  | Uniform Resource Locator  |
| DDP  | Dynamic Document Property  |
| DPP  | Dynamic Process Property  |
