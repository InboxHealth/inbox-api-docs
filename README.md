
# Inbox Health Partner API

This document is meant to accompany and provide a user-friendly overview of the full specifications of the Inbox Health Partner REST API, fully-documented at inboxhealth.com/api.  Reading and understand the data model and endpoints outlined by those full specifications is recommended.

## Introduction

Logging in to our Partner Portal at inboxhealth.com/partner will immediately bring you to your "Account Settings" page. To get started authenticating yourself to our REST API, you'll need to generate your user account's API Key. At the bottom left of the "Account Settings" page, click the "View API Key" button on the left and re-enter your password to see your Inbox Health API Key. Keep this key in a safe place, preferably in a secure key store, as it grants full access to the Inbox Health API and can access any of the Inbox Health data managed by medical enterprises under your control.

The full specification of the Inbox Health Partner REST API documentation is available at [demo.inboxhealth.com/api](http://demo.inboxhealth.com/api) .  This page, automatically generated by OpenAPI (formerly known as the Swagger Specification) has all of the main model resources listed on the page should expand with the valid operations that can be performed against each one.  While logged into the partner portal, notice that you can perform any of the API actions by supplying parameters and hitting the "Try It." This works because the API falls back to cookie-based authentication if the "Authorization" HTTP Header is not present. Feel free to experiment with these, but also note that the User Interface at [demo.inboxhealth.com/partner](http://demo.inboxhealth.com/partner) also utilizes these exact requests to render your information in this UI, so feel free to use your Web Browser's Networks tab in its Developer Tools to explore how you can use some of its requests.

## Authentication
Inbox Health's API utilizes "HTTP Basic Authentication" with the API key acting as the username in each request.

Add the API Key you generated via the Partner portal above to each HTTP request as your Username via HTTP Basic Authentication.  If you are unfamiliar with this practice and do not  have a HTTP client that supports Basic Authentication on requests, you can implement yourself pretty easily by adding the header
``` 
Authorization: Basic <credentials>
```
 where `<credentials>` is your API Key with a colon suffix, base 64 encoded i.e. `<API_KEY>:` .

## Onboarding New Clients

### Creating an Enterprise
The "Enterprise" model is the central record in Inbox Health's API Entities that represents a new customer seeking to bill their patients (whether it is a Hospital, Medical Practice, Therapy Group, or other medical organization).  Thus, the first step to onboarding a new client to the Inbox Health platform is to create their Enterprise record that corresponds to their business and will serve to define many of the basic properties. For now, we will review creating a basic Enterprise with one sub "Practice" (facility) and let Inbox Health set many of the default properties for us.  Send the following HTTP Request to the Enterprise POST endpoint available at [demo.inboxhealth.com/api/partner/v2/enterprises](http://demo.inboxhealth.com/api/partner/v2/enterprises)  

JSON Body:

```
{  
	"enterprise": {  
		"name": "City of New Haven University Hospital",  
		"city": "New Haven",  
		"state": "CT",  
		"address_line_1": "770 Chapel St",  
		"address_line_2": null,  
		"zip": "06512",  
		"support_phone_number": "(203) 415-3486",  
		"sales_tax": 0,  
		"default_quick_pay_description": "Copay",  
		"logo_background_color": null,  
		"default_checkin_routes": null,  
		"statement_descriptor": "BANK STATEMENT DESCRIPTOR OVERRIDE",  
		"time_zone": "Eastern Time (US & Canada)",  
		"color_statements": true,  
		"first_class": true,  
		"return_envelope": true,  
		"perforation": true,
		"practices_attributes": [
			{  
				"name": "New Haven Emergency Room",  
				"address_line_1": "Address line 1 placeholder",  
				"city": "City Placeholder",  
				"state": "Connecticut",  
				"time_zone": "Eastern Time (US & Canada)"  
			}
		]  
	}  
}  
```
The HTTP Response returned from Inbox Health as it will look something like this:

```
```


### Creating Patients

Now that you've created your first test Enterprise, let's create the first Patient record to provide a central record to attach future Invoices (charges) and Payments.  Patient records act similar to the Customer objects in other invoicing platforms and are tracked individually; their balances and properties along with the Enterprise's settings and the Enterprise's defined BillingCycleTemplates, govern how and when Inbox Health sends the Patient statements and communication.

```
{  
	"patient":{  
		"first_name":"Test First Name",  
		"last_name":"Test Last Name",  
		"date_of_birth":"1987-07-23",  
		"sex":"Male",  
		"email":"testemail@inboxhealth.com",  
		"enterprise_id": <<Enterprise ID returned above>>  
	}  
}  
```

## Managing Patient Balances
This section covers how to create new Invoice, LineItem, and Payment records to assign, update and manage a Patient's balance in Inbox Health over time.

## Sending Statements and Communication
This section covers how to define new BillingCycleTemplates, control existing BillingCycles, and send out-of-band communication such a Patient Tickets (SMS, email, and automated voice calls)

## Subscribing to Webhooks
This section covers how to receive dynamic updates from Inbox Health via REST API webhooks that ensure API clients are immediately informed upon changes of relevant records in Inbox Health.  Whether the change originates from a patient, provider, administrator or automated system these webhooks are triggered and immediately provide feedback
 
## FAQs
Please don't hesitate to ask questions via our email, Slack or GitHub Issues.  We'll update this section with common questions as we work to flesh out our documentation.

## Forthcoming Documentation
We're currently working on more documentation, but between these initial examples and the swagger docs I hope you'll be able to get a decent start the feel of the API itself. Don't hesitate to contact us by email, GitHub Issues, or Slack for quicker responses.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA5MzUwMDAzNywtODQzMzkxODQ4LC02OD
E0NTMwMzUsMTMwMTgwMzY1Ml19
-->