# Sage Intacct Integration Sample

## Description
This repo contains a Linx 6 solution that shows how you can consume the [Sage Intacct web service](https://developer.intacct.com/web-services/). It makes use of a REST call to call the web service with an XML body. The result is a JSON object that can be manipulated and consumed by other Linx functions or processes. The solution was made to be generic enough so that it will only call the 'Query and List Customers' method with two fields. You can alter the response received by manipulating the request body and then adding those amendments to the response body. The sample also shows how a Session ID can be retrieved before any methods can be used in the Sage Intacct web service. 

You can download this sample and manipulate it to suit your integration using [Linx 6](https://linx.software/).

## Installation
This is a Linx 6 solution, so you will need an installed version of the [Linx 6 designer](https://linx.software/) to work on this solution and to add in your own logic. 

## Usage

All [authentication details (company id, user name, password, control ID, userID and more)](https://developer.intacct.com/web-services/#authentication) are placed in the settings.

The solution has 2 main functions:

#### generateAPISession: 
This function will get a Session ID. A session ID is required to interact with the web service and functions as the access token for your session. This is done by passing in your credentials and calling the [getAPISession](https://developer.intacct.com/api/company-console/api-sessions/) function of the web service. The Session ID will be passed out as the result of this function, meaning that it can be reused in other functions that need a Session ID to interact with the web service.

#### getCustomers:
This function will call the [Query and List Customers](https://developer.intacct.com/api/accounts-receivable/customers/#query-and-list-customers) method. It takes into account that the web service may need to be called more than once (paging) if there are more than the limit amount of records to be retrieved. The function was developed to retrieve only two fields; however, it can be altered to retrieve the specific fields that you need. To do this, the fields need to be added to the 'select' property in the request type. You will also need to change the response type (Customer_Response) and add your fields. It is recommended that you import a new type for the altered response type as some fields contain., which will be imported as _ and the ASCII value 46 (example _46). However you decide to name these new fields in the Response type, you can map them in the JSONReader function by altering the Property map. There you can ensure that the fields are mapped to their corresponding property in the Response type (Customer_Response).
The result of this funciton is a list of customer records based on your search parameters (the data when they were modified). You can use this list however you need (read to a database, make available via API, add to a report or even integrate into another system). This development can be done in Linx 6.
Please note that this function expects an input parameter, WHENMODIFIED, which will retrieve a list of customers that was modified on that specific date. You can add additional filter conditions by altering the filter property.

For more details, view our blog post on integrating Sage Intacct with Linx. 

## Contributing

For questions please ask the [Linx community](https://linx/software/community) or use the [Slack channel](https://linxsoftware.slack.com/archives/C01FLBC1XNX). 

## License

[MIT](https://github.com/linx-software/template-repo/blob/main/LICENSE.txt)
