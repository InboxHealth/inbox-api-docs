
# Inbox Health Partner API

This document is meant to accompany and provide a user-friendly overview of the full specifications of the Inbox Health Partner REST API, fully-documented at [rest.demo.inboxhealth.com/api](https://rest.demo.inboxhealth.com/api).  Reading and understand the data model and endpoints outlined by those full specifications is recommended.

## Introduction

Logging in to our Partner Portal at [partner.demo.inboxhealth.com](https://partner.demo.inboxhealth.com) will immediately bring you to your "Account Settings" page. To get started authenticating yourself to our REST API, you'll need to generate your user account's API Key. At the bottom left of the "Account Settings" page, click the "View API Key" button on the left and re-enter your password to see your Inbox Health API Key. Keep this key in a safe place, preferably in a secure key store, as it grants full access to the Inbox Health API and can access any of the Inbox Health data managed by medical enterprises under your control.

The full specification of the Inbox Health Partner REST API documentation is available at [rest.demo.inboxhealth.com/api](https://rest.demo.inboxhealth.com/api) .  This page, automatically generated by OpenAPI (formerly known as the Swagger Specification) has all of the main model resources listed on the page should expand with the valid operations that can be performed against each one.  While logged into the partner portal, notice that you can perform any of the API actions by supplying parameters and hitting the "Try It." This works because the API falls back to cookie-based authentication if the "Authorization" HTTP Header is not present. Feel free to experiment with these, but also note that the User Interface at [partner.demo.inboxhealth.com](https://partner.demo.inboxhealth.com) also utilizes these exact requests to render your information in this UI, so feel free to use your Web Browser's Networks tab in its Developer Tools to explore how you can use some of its requests.

## Authentication
In order for your request to be properly authenticated, you will need to supply your API Key as a header in each request you send. Simply add the API Key you generated via the Partner portal above to each HTTP request in a `x-api-key` header.

## Rate Limiting
By default, all Partner API users are assigned a Basic Partner usage plan that is rate limited to 1 request per second, with an available burst rate of 40 requests per second. 

## Onboarding New Clients

### Creating an Enterprise
The "Enterprise" model is the central record in Inbox Health's API Entities that represents a new customer seeking to bill their patients (whether it is a Hospital, Medical Practice, Therapy Group, or other medical organization).  Thus, the first step to onboarding a new client to the Inbox Health platform is to create their Enterprise record that corresponds to their business and will serve to define many of the basic properties. For now, we will review creating a basic Enterprise with one sub "Practice" (facility) and let Inbox Health set many of the default properties for us.  Send the following HTTP Request to the Enterprise POST endpoint available at [api.demo.inboxhealth.com/partner/v2/enterprises](http://api.demo.inboxhealth.com/partner/v2/enterprises)  

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
{
    "enterprise": {
        "id": 47,
        "name": "City of New Haven University Hospital",
        "created_at": "2019-10-17T14:26:00.497Z",
        "updated_at": "2019-10-17T14:26:04.022Z",
        "enterprise_plan_id": 9,
        "bank_name": null,
        "bank_last_4": null,
        "country": null,
        "address_line_1": "770 Chapel St",
        "address_line_2": null,
        "city": "New Haven",
        "state": "CT",
        "ein": null,
        "transfer_date_scheduled": null,
        "transfer_status": "scheduled",
        "transfer_interval": null,
        "enterprise_payment_date_scheduled": null,
        "billing_name": null,
        "minimum_bill_amount_cents": 0,
        "support_phone_number": "(203) 415-3486",
        "use_support_phone_number": false,
        "payment_phone_number": null,
        "default_service_code": "30",
        "additional_fees_description": null,
        "additional_fees_cents": 0,
        "sales_tax": 0.0,
        "default_service_location": "11",
        "zip": "06512",
        "default_statement_memo": null,
        "days_before_patient_balance_reminder": 15,
        "days_before_patient_balance_reminder_with_paper_statements": 30,
        "enterprise_plan": {
            "id": 9,
            "plan_name": "Basic (Freemium)",
            "created_at": "2019-05-09T17:49:11.038Z",
            "updated_at": "2019-05-09T17:49:11.038Z",
            "per_eligibility_benefit_rate_cents": 25,
            "eligibility_benefits_per_month": 0,
            "monthly_fee_cents": 0,
            "custom": false,
            "check_fee_cents": 0,
            "card_transaction_rate": 0.022,
            "amex_transaction_rate": 0.035,
            "amex_debit_transaction_rate": 0.029,
            "amex_prepaid_transaction_rate": 0.029,
            "amex_credit_transaction_rate": 0.029,
            "discover_debit_transaction_rate": 0.029,
            "discover_prepaid_transaction_rate": 0.029,
            "discover_credit_transaction_rate": 0.029,
            "mastercard_debit_transaction_rate": 0.022,
            "mastercard_prepaid_transaction_rate": 0.022,
            "mastercard_credit_transaction_rate": 0.022,
            "visa_debit_transaction_rate": 0.022,
            "visa_prepaid_transaction_rate": 0.022,
            "visa_credit_transaction_rate": 0.022,
            "terminal_amex_debit_transaction_rate": 0.029,
            "terminal_amex_prepaid_transaction_rate": 0.029,
            "terminal_amex_credit_transaction_rate": 0.029,
            "terminal_discover_debit_transaction_rate": 0.029,
            "terminal_discover_prepaid_transaction_rate": 0.029,
            "terminal_discover_credit_transaction_rate": 0.029,
            "terminal_mastercard_debit_transaction_rate": 0.022,
            "terminal_mastercard_prepaid_transaction_rate": 0.022,
            "terminal_mastercard_credit_transaction_rate": 0.022,
            "terminal_visa_debit_transaction_rate": 0.022,
            "terminal_visa_prepaid_transaction_rate": 0.022,
            "terminal_visa_credit_transaction_rate": 0.022,
            "amex_debit_transaction_flat_fee_cents": 30,
            "amex_prepaid_transaction_flat_fee_cents": 30,
            "amex_credit_transaction_flat_fee_cents": 30,
            "discover_debit_transaction_flat_fee_cents": 30,
            "discover_prepaid_transaction_flat_fee_cents": 30,
            "discover_credit_transaction_flat_fee_cents": 30,
            "mastercard_debit_transaction_flat_fee_cents": 30,
            "mastercard_prepaid_transaction_flat_fee_cents": 30,
            "mastercard_credit_transaction_flat_fee_cents": 30,
            "visa_debit_transaction_flat_fee_cents": 30,
            "visa_prepaid_transaction_flat_fee_cents": 30,
            "visa_credit_transaction_flat_fee_cents": 30,
            "terminal_amex_debit_transaction_flat_fee_cents": 30,
            "terminal_amex_prepaid_transaction_flat_fee_cents": 30,
            "terminal_amex_credit_transaction_flat_fee_cents": 30,
            "terminal_discover_debit_transaction_flat_fee_cents": 30,
            "terminal_discover_prepaid_transaction_flat_fee_cents": 30,
            "terminal_discover_credit_transaction_flat_fee_cents": 30,
            "terminal_mastercard_debit_transaction_flat_fee_cents": 30,
            "terminal_mastercard_prepaid_transaction_flat_fee_cents": 30,
            "terminal_mastercard_credit_transaction_flat_fee_cents": 30,
            "terminal_visa_debit_transaction_flat_fee_cents": 30,
            "terminal_visa_prepaid_transaction_flat_fee_cents": 30,
            "terminal_visa_credit_transaction_flat_fee_cents": 30,
            "ach_transaction_rate": 0.019,
            "ach_transaction_flat_fee_cents": 0,
            "inbox_health_transaction_rate": 0.017,
            "transaction_flat_fee_cents": 30,
            "stripe_plan_id": "basic",
            "number_of_users": 1,
            "per_email_rate_cents": 0,
            "per_paper_rate_cents": 125,
            "per_voice_call_minute_rate_cents": 0,
            "per_sms_rate_cents": 1,
            "enable_preauth": true,
            "enable_estimates": true,
            "enable_billing": true,
            "enable_checkin": false,
            "enable_eligibility": true,
            "enable_full_service": false
        },
        "stripe_fields_needed": null,
        "has_stripe_subscription": false,
        "estimate_down_payment_rate": 0.2,
        "bcbs_payer_id": null,
        "default_quick_pay_description": "Copay",
        "enable_scheduled_eligible_requests": true,
        "logo_background_color": null,
        "default_checkin_routes": "{\"checkIn.confirmAppointmentDetails\":{\"next\":\"checkIn.patientReview\"},\"checkIn.patientReview\":{\"next\":\"checkIn.patientMoreAboutYou\",\n    \"prev\":\"checkIn.confirmAppointmentDetails\"},\"checkIn.patientMoreAboutYou\":{\"next\":\"checkIn.patientContactInformation\",\"prev\":\"checkIn.patientReview\"},\n    \"checkIn.patientContactInformation\":{\"next\":\"checkIn.patientAddress\",\"prev\":\"checkIn.patientMoreAboutYou\"},\n    \"checkIn.patientAddress\":{\"next\":\"checkIn.emergencyContact\",\"prev\":\"checkIn.patientContactInformation\"},\n    \"checkIn.emergencyContact\":{\"next\":\"checkIn.terms\",\"prev\":\"checkIn.patientAddress\"},\n    \"checkIn.terms\":{\"next\":\"checkIn.confirmInsurance\",\"prev\":\"checkIn.emergencyContact\"},\"checkIn.confirmInsurance\":{\"prev\":\"checkIn.terms\"}}",
        "gift_card_merchant_number": null,
        "gift_card_user_name": null,
        "enable_giftcards": false,
        "statement_descriptor": "HOSPITAL FEE",
        "has_logo_base64": false,
        "cancellation_fee_window": 0,
        "cancellation_fee_cents": 0,
        "reschedule_window": 30,
        "soonest_bookable_time_window": 30,
        "apply_payment": true,
        "default_eligible_npi": null,
        "checkin_card_on_file_required": false,
        "patient_billing_active": true,
        "auto_charge": false,
        "auto_charge_max_cents": 0,
        "past_due_balance_days": 45,
        "collection_warning_balance_days": 90,
        "enable_scheduled_appointment_reminders": false,
        "max_paper_bills_per_billing_cycle_count": 3,
        "soft_delete": false,
        "billing_business_name": null,
        "billing_address_line_1": null,
        "billing_address_line_2": null,
        "billing_city": null,
        "billing_state": null,
        "billing_zip": null,
        "time_zone": "Eastern Time (US & Canada)",
        "billing_contact_email": null,
        "baa_agree": false,
        "baa_agreed_at": null,
        "baa_html": null,
        "has_baa_signature_base64": false,
        "send_initial_statement_sms": false,
        "default_billing_cycle_template_id": 1,
        "twenty_four_hours_appt_reminders": true,
        "fourty_eight_hours_appt_reminders": false,
        "one_week_appt_reminders": true,
        "make_checks_payable_to": null,
        "custom_collection_copy": null,
        "legacy_payer_model": false,
        "enable_advanced_payment_routing": false,
        "self_pay_imported_payer_id": null,
        "enable_unapplied_payment_only": false,
        "post_checkin_message": null,
        "enable_simplified_account_view": false,
        "accepts_credit_card": true,
        "color_statements": true,
        "first_class": true,
        "return_envelope": true,
        "perforation": true,
        "patient_support_email": null,
        "portal_accepts_credit_card": true,
        "portal_accepts_ach": false,
        "links": {
            "practices": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/practices",
            "patients": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/patients",
            "enterprise_invoices": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/enterprise_invoices",
            "enterprise_payment_infos": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/enterprise_payment_infos",
            "enterprise_payments": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/enterprise_payments",
            "transfers": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/transfers",
            "admin_organizations": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/admin_organizations",
            "doctors": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/doctors",
            "appointment_templates": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/appointment_templates",
            "payment_reasons": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/payment_reasons",
            "api_integrations": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/api_integrations",
            "billing_cycle_templates": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/billing_cycle_templates",
            "write_off_codes": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/write_off_codes",
            "deposit_accounts": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/deposit_accounts",
            "card_readers": "https://demo.inboxhealth.com/api/partner/v2/enterprises/47/card_readers"
        }
    }
}
```

Most importantly, store the `enterprise.id` field as this will serve as the unique identifier for this record and form the basis for many other requests for associated records.

### Creating Patients

Now that you've created your first test Enterprise, let's create the first Patient record to provide a central record to attach future Invoices (charges) and Payments.  Patient records act similar to Customer objects seen in other invoicing platforms and are tracked individually; their balances and properties along with the Enterprise's settings and the Enterprise's defined BillingCycleTemplates, govern how and when Inbox Health sends the Patient statements and communication.

```
{  
	"patient":{  
		"first_name":"Test First Name",  
		"last_name":"Test Last Name",  
		"date_of_birth":"1987-07-23",  
		"sex":"Male",  
		"email":"testemail@inboxhealth.com",  
		"enterprise_id": 47  
	}  
}  
```
Note that the Enterprise ID (47 in the example case above) should be the ID you stored from the prior Enterprise POST request.

## Managing Patient Balances
This section covers how to create new Invoice, LineItem, and Payment records to assign, update and manage a Patient's balance in Inbox Health over time.

## Sending Statements and Communication
This section covers how to define new BillingCycleTemplates, control existing BillingCycles, and send out-of-band communication such a Patient Tickets (SMS, email, and automated voice calls)

## Subscribing to Webhooks
This section covers how to receive dynamic updates from Inbox Health via REST API webhooks that ensure API clients are immediately informed upon changes of relevant records in Inbox Health.  Whether the change originates from a patient, provider, administrator or automated system these webhooks are triggered and immediately provide feedback

## X-InboxHealth-Signature Header
This section will explain the steps required to reproduce the header X-InboxHealth-Signature which is used to verify that all webhook event requests coming from Inbox Health are authentic and haven’t been tampered with. The X-InboxHealth-Signature header is generated using the HMAC-SHA1 hashing algorithm, with the base signature being generated from the request URL and the POST body parameters, using your secret API key as the signing key. 

The webhook event we will be demonstrating with will be a `patient_created` event with dummy JSON data to represent what a typical event would actually look like. The raw request looks like this

```
POST https://coolcompany.com/api/v1/webhooks
Content-Type: application/json
Host: coolcompany.com
Body: {"id":4805,"livemode":false,"created_at":"2019-08-29T11:00:26.000-04:00","event_type":"patient_created","event_data":{"object":{"id":1,"user_id":null,"enterprise_id":1,"first_name":"Ed","middle_name":"E","last_name":"Edison","created_at":"2019-08-24T23:08:14.691Z","updated_at":"2019-08-25T10:06:48.507Z","address_line_1":"123 Mansion Rd","address_line_2":null,"city":"Thimbleweed Park","state":"WA","cell_phone":"(555) 555-5555","secondary_phone":"(555) 555-5555","date_of_birth":"1987-10-05","primary":true,"ssn":"801-31-3292","sex":"Male","removed":false,"email":"ed@edison.com","zip":"06510","email_two":null,"health_record_id":"3425","notes":null,"balance_cents":8940,"soft_delete":0,"patient_plan_ids":[1],"last_notified_at":"2014-08-30T19:00:00.000Z","race":null,"language":"English","ethnicity":null,"marital_status":"Single","employment_status":null,"employer_name":null,"contact_preference":"both","occupation":null,"pharmacy_name":null,"pharmacy_address_line_1":null,"pharmacy_address_line_2":null,"pharmacy_city":null,"pharmacy_state":null,"pharmacy_phone_number":null,"maiden_name":null,"home_phone":null,"work_phone":"(555) 555-5555","practice_id":13,"sms_opt_out":false,"phone_opt_out":false,"emergency_contacts":[],"external_ids":[{"id":1,"issuer":"coolpm","external_id":"3425"}],"statement_cycle_started_at":null,"collection_warning_letter_date":null,"needs_card_update":false,"corrected_address_line_1":null,"corrected_address_line_2":null,"corrected_city":null,"corrected_state":null,"corrected_zip":null,"links":{"invoices":null,"payments":null,"notifications":null,"patient_payment_infos":null,"tickets":null},"object":"patient"}}}
```

#### Collecting the Request URL

All webhook events sent by InboxHealth will be via a POST HTTP Method. The exact URL of the request is used as part of the base signature. So in our current example, the URL used would be https://coolcompany.com/api/v1/webhooks

#### Collecting Parameters

The second part of creating the base signature is collecting the request parameters, which are sorted and concatenated into a normalized string using the following rules:

URL encode every key and value
Parameters are sorted by name, using lexicographical byte value ordering. If two or more parameters share the same name, they are sorted by their value
Parameters are concatenated in their sorted order into a single string. For each parameter, the name is separated from the corresponding value by an '=' character (ASCII code 61), even if the value is empty. Each name-value pair is separated by an '&' character (ASCII code 38)

Given our example POST body above, these parameters would be normalized into the following single string

```
created_at=2019-08-29T12%3A06%3A53.000-04%3A00&event_data%5Bobject%5D%5Baddress_line_1%5D=123%20Mansion%20Rd&event_data%5Bobject%5D%5Baddress_line_2%5D=&event_data%5Bobject%5D%5Bbalance_cents%5D=0&event_data%5Bobject%5D%5Bcell_phone%5D=%28555%29%20555-5555&event_data%5Bobject%5D%5Bcity%5D=Thimbleweed%20Park&event_data%5Bobject%5D%5Bcollection_warning_letter_date%5D=&event_data%5Bobject%5D%5Bcontact_preference%5D=both&event_data%5Bobject%5D%5Bcorrected_address_line_1%5D=&event_data%5Bobject%5D%5Bcorrected_address_line_2%5D=&event_data%5Bobject%5D%5Bcorrected_city%5D=&event_data%5Bobject%5D%5Bcorrected_state%5D=&event_data%5Bobject%5D%5Bcorrected_zip%5D=&event_data%5Bobject%5D%5Bcreated_at%5D=2019-08-24T23%3A08%3A14.691Z&event_data%5Bobject%5D%5Bdate_of_birth%5D=1987-10-07&event_data%5Bobject%5D%5Bemail%5D=weirded%40edisons.com&event_data%5Bobject%5D%5Bemail_two%5D=&event_data%5Bobject%5D%5Bemployer_name%5D=&event_data%5Bobject%5D%5Bemployment_status%5D=&event_data%5Bobject%5D%5Benterprise_id%5D=10&event_data%5Bobject%5D%5Bethnicity%5D=&event_data%5Bobject%5D%5Bfirst_name%5D=Ed&event_data%5Bobject%5D%5Bhealth_record_id%5D=12345&event_data%5Bobject%5D%5Bhome_phone%5D=&event_data%5Bobject%5D%5Bid%5D=669&event_data%5Bobject%5D%5Blanguage%5D=English&event_data%5Bobject%5D%5Blast_name%5D=Edison&event_data%5Bobject%5D%5Blast_notified_at%5D=&event_data%5Bobject%5D%5Blinks%5D%5Binvoices%5D=&event_data%5Bobject%5D%5Blinks%5D%5Bnotifications%5D=&event_data%5Bobject%5D%5Blinks%5D%5Bpatient_payment_infos%5D=&event_data%5Bobject%5D%5Blinks%5D%5Bpayments%5D=&event_data%5Bobject%5D%5Blinks%5D%5Btickets%5D=&event_data%5Bobject%5D%5Bmaiden_name%5D=&event_data%5Bobject%5D%5Bmarital_status%5D=Single&event_data%5Bobject%5D%5Bmiddle_name%5D=E&event_data%5Bobject%5D%5Bneeds_card_update%5D=false&event_data%5Bobject%5D%5Bnotes%5D=&event_data%5Bobject%5D%5Bobject%5D=patient&event_data%5Bobject%5D%5Boccupation%5D=&event_data%5Bobject%5D%5Bpharmacy_address_line_1%5D=&event_data%5Bobject%5D%5Bpharmacy_address_line_2%5D=&event_data%5Bobject%5D%5Bpharmacy_city%5D=&event_data%5Bobject%5D%5Bpharmacy_name%5D=&event_data%5Bobject%5D%5Bpharmacy_phone_number%5D=&event_data%5Bobject%5D%5Bpharmacy_state%5D=&event_data%5Bobject%5D%5Bphone_opt_out%5D=false&event_data%5Bobject%5D%5Bpractice_id%5D=13&event_data%5Bobject%5D%5Bprimary%5D=true&event_data%5Bobject%5D%5Brace%5D=&event_data%5Bobject%5D%5Bremoved%5D=false&event_data%5Bobject%5D%5Bsecondary_phone%5D=%28555%29%20555-5555&event_data%5Bobject%5D%5Bsex%5D=Male&event_data%5Bobject%5D%5Bsms_opt_out%5D=false&event_data%5Bobject%5D%5Bsoft_delete%5D=0&event_data%5Bobject%5D%5Bssn%5D=801-31-3292&event_data%5Bobject%5D%5Bstate%5D=WA&event_data%5Bobject%5D%5Bstatement_cycle_started_at%5D=&event_data%5Bobject%5D%5Bupdated_at%5D=2019-08-25T10%3A06%3A48.507Z&event_data%5Bobject%5D%5Buser_id%5D=&event_data%5Bobject%5D%5Bwork_phone%5D=%28555%29%20555-5555&event_data%5Bobject%5D%5Bzip%5D=06510&event_type=patient_created&id=4806&livemode=false
```

For readability purposes, the normalized parameters split into an array would be as follows

```
[0] = "created_at=2019-08-29T12%3A06%3A53.000-04%3A00"
[1] = "event_data%5Bobject%5D%5Baddress_line_1%5D=123%20Mansion%20Rd"
[2] = "event_data%5Bobject%5D%5Baddress_line_2%5D="
[3] = "event_data%5Bobject%5D%5Bbalance_cents%5D=0"
[4] = "event_data%5Bobject%5D%5Bcell_phone%5D=%28555%29%20555-5555"
[5] = "event_data%5Bobject%5D%5Bcity%5D=Thimbleweed%20Park"
[6] = "event_data%5Bobject%5D%5Bcollection_warning_letter_date%5D="
[7] = "event_data%5Bobject%5D%5Bcontact_preference%5D=both"
[8] = "event_data%5Bobject%5D%5Bcorrected_address_line_1%5D="
[9] = "event_data%5Bobject%5D%5Bcorrected_address_line_2%5D="
[10] = "event_data%5Bobject%5D%5Bcorrected_city%5D="
[11] = "event_data%5Bobject%5D%5Bcorrected_state%5D="
[12] = "event_data%5Bobject%5D%5Bcorrected_zip%5D="
[13] = "event_data%5Bobject%5D%5Bcreated_at%5D=2019-08-24T23%3A08%3A14.691Z"
[14] = "event_data%5Bobject%5D%5Bdate_of_birth%5D=1987-10-07"
[15] = "event_data%5Bobject%5D%5Bemail%5D=weirded%40edisons.com"
[16] = "event_data%5Bobject%5D%5Bemail_two%5D="
[17] = "event_data%5Bobject%5D%5Bemployer_name%5D="
[18] = "event_data%5Bobject%5D%5Bemployment_status%5D="
[19] = "event_data%5Bobject%5D%5Benterprise_id%5D=10"
[20] = "event_data%5Bobject%5D%5Bethnicity%5D="
[21] = "event_data%5Bobject%5D%5Bfirst_name%5D=Ed"
[22] = "event_data%5Bobject%5D%5Bhealth_record_id%5D=12345"
[23] = "event_data%5Bobject%5D%5Bhome_phone%5D="
[24] = "event_data%5Bobject%5D%5Bid%5D=669"
[25] = "event_data%5Bobject%5D%5Blanguage%5D=English"
[26] = "event_data%5Bobject%5D%5Blast_name%5D=Edison"
[27] = "event_data%5Bobject%5D%5Blast_notified_at%5D="
[28] = "event_data%5Bobject%5D%5Blinks%5D%5Binvoices%5D="
[29] = "event_data%5Bobject%5D%5Blinks%5D%5Bnotifications%5D="
[30] = "event_data%5Bobject%5D%5Blinks%5D%5Bpatient_payment_infos%5D="
[31] = "event_data%5Bobject%5D%5Blinks%5D%5Bpayments%5D="
[32] = "event_data%5Bobject%5D%5Blinks%5D%5Btickets%5D="
[33] = "event_data%5Bobject%5D%5Bmaiden_name%5D="
[34] = "event_data%5Bobject%5D%5Bmarital_status%5D=Single"
[35] = "event_data%5Bobject%5D%5Bmiddle_name%5D=E"
[36] = "event_data%5Bobject%5D%5Bneeds_card_update%5D=false"
[37] = "event_data%5Bobject%5D%5Bnotes%5D="
[38] = "event_data%5Bobject%5D%5Bobject%5D=patient"
[39] = "event_data%5Bobject%5D%5Boccupation%5D="
[40] = "event_data%5Bobject%5D%5Bpharmacy_address_line_1%5D="
[41] = "event_data%5Bobject%5D%5Bpharmacy_address_line_2%5D="
[42] = "event_data%5Bobject%5D%5Bpharmacy_city%5D="
[43] = "event_data%5Bobject%5D%5Bpharmacy_name%5D="
[44] = "event_data%5Bobject%5D%5Bpharmacy_phone_number%5D="
[45] = "event_data%5Bobject%5D%5Bpharmacy_state%5D="
[46] = "event_data%5Bobject%5D%5Bphone_opt_out%5D=false"
[47] = "event_data%5Bobject%5D%5Bpractice_id%5D=13"
[48] = "event_data%5Bobject%5D%5Bprimary%5D=true"
[49] = "event_data%5Bobject%5D%5Brace%5D="
[50] = "event_data%5Bobject%5D%5Bremoved%5D=false"
[51] = "event_data%5Bobject%5D%5Bsecondary_phone%5D=%28555%29%20555-5555"
[52] = "event_data%5Bobject%5D%5Bsex%5D=Male"
[53] = "event_data%5Bobject%5D%5Bsms_opt_out%5D=false"
[54] = "event_data%5Bobject%5D%5Bsoft_delete%5D=0"
[55] = "event_data%5Bobject%5D%5Bssn%5D=801-31-3292"
[56] = "event_data%5Bobject%5D%5Bstate%5D=WA"
[57] = "event_data%5Bobject%5D%5Bstatement_cycle_started_at%5D="
[58] = "event_data%5Bobject%5D%5Bupdated_at%5D=2019-08-25T10%3A06%3A48.507Z"
[59] = "event_data%5Bobject%5D%5Buser_id%5D="
[60] = "event_data%5Bobject%5D%5Bwork_phone%5D=%28555%29%20555-5555"
[61] = "event_data%5Bobject%5D%5Bzip%5D=06510"
[62] = "event_type=patient_created"
[63] = "id=4806"
[64] = "livemode=false"
```

Since we based our normalization rules off of the OAuth specification, we leverage the OAuth Ruby library for normalizing the parameters. The method can be viewed on GitHub at https://github.com/oauth-xx/oauth-ruby/blob/master/lib/oauth/helper.rb#L44 for further education on the normalizing process. 

#### The Signing Key

Your secret Inbox Health user API key is used as the signing key to the HMAC-SHA1 hashing algorithm. We determine which API key to sign with _based on the user that created, or last updated, the webhook endpoint in the Inbox Health Partner app._ As always, keep this key secret and safe!

#### Calculating the Signature

We can now calculate the final signature by passing the base string of our request URL and normalized request parameters to the HMAC-SHA1 hashing algorithm, using the user API key as the signing key. Please note, HMAC will output in binary string, so we convert it to base64. 

Given the following base signature

```
https://coolcompany.com/api/v1/webhookscreated_at=2019-08-29T12%3A06%3A53.000-04%3A00&event_data%5Bobject%5D%5Baddress_line_1%5D=123%20Mansion%20Rd&event_data%5Bobject%5D%5Baddress_line_2%5D=&event_data%5Bobject%5D%5Bbalance_cents%5D=0&event_data%5Bobject%5D%5Bcell_phone%5D=%28555%29%20555-5555&event_data%5Bobject%5D%5Bcity%5D=Thimbleweed%20Park&event_data%5Bobject%5D%5Bcollection_warning_letter_date%5D=&event_data%5Bobject%5D%5Bcontact_preference%5D=both&event_data%5Bobject%5D%5Bcorrected_address_line_1%5D=&event_data%5Bobject%5D%5Bcorrected_address_line_2%5D=&event_data%5Bobject%5D%5Bcorrected_city%5D=&event_data%5Bobject%5D%5Bcorrected_state%5D=&event_data%5Bobject%5D%5Bcorrected_zip%5D=&event_data%5Bobject%5D%5Bcreated_at%5D=2019-08-24T23%3A08%3A14.691Z&event_data%5Bobject%5D%5Bdate_of_birth%5D=1987-10-07&event_data%5Bobject%5D%5Bemail%5D=weirded%40edisons.com&event_data%5Bobject%5D%5Bemail_two%5D=&event_data%5Bobject%5D%5Bemployer_name%5D=&event_data%5Bobject%5D%5Bemployment_status%5D=&event_data%5Bobject%5D%5Benterprise_id%5D=10&event_data%5Bobject%5D%5Bethnicity%5D=&event_data%5Bobject%5D%5Bfirst_name%5D=Ed&event_data%5Bobject%5D%5Bhealth_record_id%5D=12345&event_data%5Bobject%5D%5Bhome_phone%5D=&event_data%5Bobject%5D%5Bid%5D=669&event_data%5Bobject%5D%5Blanguage%5D=English&event_data%5Bobject%5D%5Blast_name%5D=Edison&event_data%5Bobject%5D%5Blast_notified_at%5D=&event_data%5Bobject%5D%5Blinks%5D%5Binvoices%5D=&event_data%5Bobject%5D%5Blinks%5D%5Bnotifications%5D=&event_data%5Bobject%5D%5Blinks%5D%5Bpatient_payment_infos%5D=&event_data%5Bobject%5D%5Blinks%5D%5Bpayments%5D=&event_data%5Bobject%5D%5Blinks%5D%5Btickets%5D=&event_data%5Bobject%5D%5Bmaiden_name%5D=&event_data%5Bobject%5D%5Bmarital_status%5D=Single&event_data%5Bobject%5D%5Bmiddle_name%5D=E&event_data%5Bobject%5D%5Bneeds_card_update%5D=false&event_data%5Bobject%5D%5Bnotes%5D=&event_data%5Bobject%5D%5Bobject%5D=patient&event_data%5Bobject%5D%5Boccupation%5D=&event_data%5Bobject%5D%5Bpharmacy_address_line_1%5D=&event_data%5Bobject%5D%5Bpharmacy_address_line_2%5D=&event_data%5Bobject%5D%5Bpharmacy_city%5D=&event_data%5Bobject%5D%5Bpharmacy_name%5D=&event_data%5Bobject%5D%5Bpharmacy_phone_number%5D=&event_data%5Bobject%5D%5Bpharmacy_state%5D=&event_data%5Bobject%5D%5Bphone_opt_out%5D=false&event_data%5Bobject%5D%5Bpractice_id%5D=13&event_data%5Bobject%5D%5Bprimary%5D=true&event_data%5Bobject%5D%5Brace%5D=&event_data%5Bobject%5D%5Bremoved%5D=false&event_data%5Bobject%5D%5Bsecondary_phone%5D=%28555%29%20555-5555&event_data%5Bobject%5D%5Bsex%5D=Male&event_data%5Bobject%5D%5Bsms_opt_out%5D=false&event_data%5Bobject%5D%5Bsoft_delete%5D=0&event_data%5Bobject%5D%5Bssn%5D=801-31-3292&event_data%5Bobject%5D%5Bstate%5D=WA&event_data%5Bobject%5D%5Bstatement_cycle_started_at%5D=&event_data%5Bobject%5D%5Bupdated_at%5D=2019-08-25T10%3A06%3A48.507Z&event_data%5Bobject%5D%5Buser_id%5D=&event_data%5Bobject%5D%5Bwork_phone%5D=%28555%29%20555-5555&event_data%5Bobject%5D%5Bzip%5D=06510&event_type=patient_created&id=4806&livemode=false
```

and using an example API key of `api_key` as our signing key, the X-InboxHealth-Signature would be

`93G+w7p0GC2FB+us2KO8lT/XfZM=`
 
## FAQs
Please don't hesitate to ask questions via our email, Slack or GitHub Issues.  We'll update this section with common questions as we work to flesh out our documentation.

## Forthcoming Documentation
We're currently working on more documentation, but between these initial examples and the swagger docs I hope you'll be able to get a decent feel of the API itself. Don't hesitate to contact us by email, GitHub Issues, or Slack for quicker responses.
