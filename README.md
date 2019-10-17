
# Inbox Health Partner API

## Introduction

Logging in to our Partner Portal at inboxhealth.com/partner will immediately bring you to your "Account Settings" page. To get started authenticating yourself to our REST API, you'll need to generate your user account's API Key. At the bottom left of the "Account Settings" page, click the "View API Key" button on the left and re-enter your password to see your Inbox Health API Key. Keep this key in a safe place, preferably in a secure key store, as it grants full access to the Inbox Health API and can access any of the Inbox Health data managed by medical enterprises under your control by simply by adding key to as your Username using HTTP Basic Authentication. If your HTTP client library does not support Basic Authentication on requests out of the box, you can implement yourself pretty easily by adding the header
``` 
Authorization: Basic <credentials>
```

 where `<credentials>` is a base64 encoded `"${API_KEY}:"` . Let me know if you have any trouble with this step

  

After logging in, you should be able to go our partner documentation page at [demo.inboxhealth.com/api](http://demo.inboxhealth.com/api) . This page can take a little while to load as the Swagger UI pulls in the documentation directly from the endpoints, but after all the requests have finished, each of the main model resources listed on the page should expand with the valid operations that can be performed against each one. You'll notice that you can perform any of the API actions by supplying parameters and hitting the "Try It." This works because the API falls back to cookie-based authentication if the "Authorization" HTTP Header is not present. Feel free to experiment with these, but also note that the User Interface at [demo.inboxhealth.com/partner](http://demo.inboxhealth.com/partner) also utilizes these exact requests to render your information in this UI, so feel free to use your Web Browser's Networks tab in its Developer Tools to explore how you can use some of its requests.

  

This documentation and these endpoints are still actively being developed, so if anything doesn't make sense don't be shy about reaching out.

  

I'll be emailing you a detailed instructions that document the first use case, which would outline how to POST and create first an "Enterprise" along with its child "Practices" (locations) using the POST /enterprises resource, and then how to subsequently post new "Patient" models that belong to that Enterprise. For now, I'd recommend trying to send a basic Enterprise with one sub "Practice" (facility) to the following endpoint:  

  

[demo.inboxhealth.com/api/partner/v2/enterprises](http://demo.inboxhealth.com/api/partner/v2/enterprises)  

  

  

JSON Body:

  

  

{  
"enterprise": {  
"name": "Mental Health/Substance Abuse Medical ",  
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

"practices_attributes": [{  
"name": "My First Mental Health Facility",  
"address_line_1": "Address line 1 placeholder",  
"city": "City Placeholder",  
"state": "New York",  
"time_zone": "Eastern Time (US & Canada)"  
}]  
}  
}  

  

After this request is successful, you could try adding patients to this medical enterprise with the following Post:

  

{  
"patient":{  
"first_name":"Test First Name",  
"last_name":"Test Last Name",  
"date_of_birth":"1987-07-23",  
"sex":"Male",  
"email":"[testemail@inboxhealth.com](mailto:testemail@inboxhealth.com)",  
"**enterprise_id**": <<Enterprise ID returned above>>  
}  
}  
  

We're currently working on more documentation, but between these initial examples and the swagger docs I hope you'll be able to get a decent start the feel of the API itself. Don't hesitate to contact us either by email or Slack for quicker responses in our new mutual channe

  

  

  

Looking forward to working with you!

## Authentication
- Logging into the Partner portal
- Generating API Keys
- Adding Authorization header to HTTP requests

## Onboarding New Users
- Creating new Enterprises and why
- 
## Creating Patients

## Assigning Patients a Balance

## Subscribing Webhooks

## FAQs

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MjAwOTEyNDcsMTMwMTgwMzY1Ml19
-->