# Salesforce REST API Connectivity using Boomi

## Problem Statement
There can be several teams in an organization who need to connect to a Salesforce organization to get/send data. Salesforce Architects usually recommend to have separate users for separate projects so that the various access levels and roles can be segregated from a security standpoint.

## Limitation of Native Salesforce Connector
Suppose if there are 7 separate users created for Boomi integration in a Salesforce organization, and we decide to use Boomi's native/out-of-box Salesforce Connector, it will cost 7 licenses and the operational cost of Boomi would increase.

## Benefits of using Salesforce REST API in Boomi Integrations
:point_right: Reduced Boomi License Cost - Since a single HTTP Connector in Boomi can be used by parameterizing the credentials of different integration users.

:point_right: Better Security - We can use OAuth 2.0 as the authentication and authorization mechanism for enhanced security.

:point_right: Faster Connectvity - Boomi's native/out-of-box Salesforce Connector conncts with the SOAP API of Salesforce, which can be slower at times, as compared to the REST API of Salesforce.

:point_right: Fsater Integration Enhancements - When we use Boomi's native/out-of-box Salesforce Connector to perform Salesforce QUERY operation, and have to update the SOQL to incorporate a new Salesforce field, we have to re-import the Salesforce Object in the Boomi's Salesforce Connector's Operation along with verifying the selected fields to avoid any additional fields being selected after the profile re-import. When we use Boomi's HTTP Connector to perform Salesforce QUERY operation, we only have to edit the parameter in the URI.

## Solution Approach 

## Create Connected App in Salesforce

## Create HTTP Client Connector in Boomi

## Salesforce QUERY Operation

## Salesforce CREATE Operation

## Salesforce UPDATE Operation

## Salesforce UPSERT Operation
