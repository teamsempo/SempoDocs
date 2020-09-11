# KoboToolbox

## What is Kobo Toolbox?

* Kobo Toolbox is a data collection tool specially designed for Humanitarian Work
* It allows for creation of sophisticated forms
* Kobo’s Android App can be used to collect data without internet
* Sempo can automatically sync with Kobo, so no manual upload is required

![](../.gitbook/assets/1uosbsmsduxnpszmb70rlzhln__ykshujdf4wnrgjta.png)

## How will we use Kobo Toolbox?

We will use three different forms:

1. **Beneficiary Enrollment** This form will be used to add each beneficiary to Sempo. 
2. **Vendor Enrollment** This form will be used to add each vendor to Sempo. 
3. **Vendor Know-Your-Customer** This form will be used to add vendor identity information to Sempo. It is separate to the Vendor Enrollment form, because we may need to collect further information about the vendor. For example, if a vendor’s drivers license does not match their bank details. This means you can re-submit this form multiple times, _as long as the Vendor Phone does not change_. 

## Creating a Kobo form

You can create your Kobo Form using Kobo’s web interface. How Sempo treats a field depends on its category.

_**Required fields**_ are fields that you **MUST** include in a form and must fill out in order for the data to be synced. The fields are not case sensitive, but they must match Sempo’s documentation. For example, for the required field “_phone_”, you CAN provide “Phone” but cannot provide “Phone number”. **But**, you can override this using XML, the ‘Data Column Name’ or some special features \(more on this later\)

_**Optional fields**_ are fields that are not required, but treated specially by Sempo. For example if you provide a “location” such as “Port Vila”, sempo will try to find the GPS location for “Port Vila”. Like required fields, you must match name in the Sempo documentation.

_**Custom fields**_ are any fields that are not **required** or **optional**. Sempo will save these fields as “Custom Attributes” for each user, allowing you to filter and group users according to this information. You can use any name you want for a custom field.

### Required Fields

For **Beneficiary and Vendor enrollment** the required fields are: 

* **“First name”:** The participant’s first name
* **“Last name”:** The participant’s last name
* _One of:_
  * **“Phone”:** The participant’s phone number \(must be a valid phone number\)
  * **“Public Serial Number”:** The ID of the Touch-to-pay card that is being given to the participant \(use the Barcode/QR Code type\)

For **Vendor KYC** the required fields are: 

* **“Phone”:** The same phone number provided in the sign up form
* **“Selfie”:** A photo of the Vendor
* **“Photo ID”:** A photo of the Vendor’s Identity Card \(Drivers License etc\)
* **“Supporting ID”:** A photo of a supporting Identity Document such a bank statement

### Optional Fields - Enrollment

There are many optional fields. The fields that might be useful are:

* **“Is Vendor”:** \(Checkbox only\) - whether the participant is a Vendor or Beneficiary. Defaults to “false” if not provided.
* **“Location”:** The text address or town of the participant, for example “Pango”
* **“GPS”:** The GPS coordinates of the participant, provided using Kobo’s “Point” field.

## Linking a form to Sempo 

### Step 1 - Get your Kobo Credentials:

{% hint style="info" %}
**Note:** your sub-domain might be different for your organisation
{% endhint %}

1. Go to your Sempo deployment \(app.withsempo.com\)
2. Click ‘Settings’ on the side bar.
3. Find the box titled ‘Kobo Toolbox Credentials’. 
4. Copy the Username and Password.

![Settings Page](../.gitbook/assets/1fxclektivcrbc2gu__psbridlcgfby0pptrlljcw7q.png)

### Step 2 - Connect your Form

1. Make sure your form is deployed on KoboToolbox.
2. In the form you would like to connect, go to ‘Settings’.
3. Next, go to ‘REST Services’
4. Click ‘Register a new service’

![](../.gitbook/assets/screen-shot-2020-09-10-at-5.25.29-pm.png)

### Step 2 - Connect your Form continued

1. Complete the following fields:
   1. Name: Sempo
   2. Endpoint URL: [https://yourdomain.withsempo.com](https://yourdomain.withsempo.com/api/v1/kobo/user/)/api/v1/user/?preprocess=true
   3. Ensure ‘Enabled’ is CHECKED
   4. Type: JSON
   5. Security: Basic Authorization
   6. Username: your username from Step 2.
   7. Password: your password from Step 2.
2. Scroll down and click ‘Create’
3. You have now connected your KoboToolbox form to Sempo!

![](../.gitbook/assets/screen-shot-2020-09-10-at-5.25.35-pm.png)

## New Kobo Integration Features

### Default Values

We now support Default values on a per-form level. This means that unlike last time, enrollers don’t need to select “is vendor”: “true” every time they sign up a person:

To add a default value, add a custom wrapper at the bottom of the “Add Rest Service” section:

![](../.gitbook/assets/screen-shot-2020-09-10-at-5.28.37-pm.png)

### Field name overrides

Any field name can be overriden on a case-by-case basis. This is useful for supporting groups, which add the group name to every field

For example if the group was “Identity Information” and the Field was “Phone”, Kobo will submit this as

“**Indentity\_Information\_Phone**”

This can be manually updated on Sempo to be recognised as just “**Phone**”. 

{% hint style="info" %}
For now, this needs to be done by a Sempo team member.
{% endhint %}
