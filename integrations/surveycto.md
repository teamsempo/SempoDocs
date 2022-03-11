# SurveyCTO

## How can Sempo integrate with SurveyCTO?

Sempo can integrate to use SurveyCTO for three forms:

1. **Participant Enrollment** This form will be used to add each beneficiary to Sempo.&#x20;
2. **Vendor Enrollment** This form will be used to add each vendor to Sempo.&#x20;
3. **Vendor Know-Your-Customer** This form will be used to add vendor identity information to Sempo. It is separate to the Vendor Enrollment form, because we may need to collect further information about the vendor. For example, if a vendor’s drivers license does not match their bank details. This means you can re-submit this form multiple times, _as long as the Vendor Phone does not change_.&#x20;

## Creating a SurveyCTO Form

Your form can have any text you wish, and they will be added as custom attributes in the enrolled users. There are a few special field names which are recognized by Sempo, and required for beneficiary and vendor enrollment.

#### Required Fields

* **“first\_name” - Text:** The participant’s first name
* **“last\_name” - Text:** The participant’s last name
* _One of:_
  * **“phone” - Text:** The participant’s phone number (must be a valid phone number)
  * **“public\_serial\_number”- Text:** The ID of the Touch-to-pay card that is being given to the participant (use the Barcode/QR Code type)

#### Optional Fields

Optional fields are fields which are not required by Sempo, but could be useful include: &#x20;

* **"location" - Text**: The text location of the user. This can be a full address, or just a town name
* **“is\_vendor” - select\_one:**  whether the participant is a Vendor or Beneficiary. Defaults to “false” if not provided.

#### Optional Fields

If there is an attribute you would like to track, but is not included in Sempo's Required or Optional fields, you can still include them in your form and have them attached to a participant on the Sempo platform! Simply create a question with any question\_id you like, and it will be used as a custom attribute.

## Creating a Form

The sempo platform is quite flexible with the data inputs it will accept from forms. You are free to design the questionnaire as you wish, so long as the required fields are present.

![](<../.gitbook/assets/image (37).png>)

Additionally, you are free to label the fields whatever you like. So long as the "name" matches the name of the required field, your integration will be supported.

![](<../.gitbook/assets/image (36).png>)

## Link a SurveyCTO form to Sempo

### Step 1 - Get your SurveyCTO Credentials:

1. Go to your Sempo deployment (app.withsempo.com)
2. Click ‘Settings’ on the side bar.
3. Find the box titled ‘Integration URL’.&#x20;
4. Ensure the "Preproces Inputs", and "Return Raw on Error" boxes are checked. &#x20;
5. Copy the integration URL from the textbox.

![Settings Page](../.gitbook/assets/settings-page.png)

#### Allow Modifications

The integration can be configured to allow modifications to existing users. If you submit a form that has the same Phone or Card ID as an existing user, it’ll update the existing user’s settings. This is useful for providing more KYC information at a later date

{% hint style="warning" %}
WARNING: This setting should only be turned on when it’s needed, as it makes it easier to accidentally use the same Touch-to-pay card twice on two different users.
{% endhint %}

To turn this setting on, ensure "Allow User Updates" is checked in step 4, in addition to the other required fields.



### Step 2 - Add Sempo as a webhook in the SurveyCTO Dashboard

Go to the Export tab in the SurveyCTO dashboard and scroll down to "Advanced: publishing form and dataset data to the cloud". Click the "OFF" button and then click "Configure" on the survey you wish to integrate.&#x20;

![](<../.gitbook/assets/image (39).png>)

Click "Add Webhook" and fill out the form. You can give it any name you wish. For "Webhook URL", paste in the URL copied from Step 1.

&#x20;![](<../.gitbook/assets/image (35).png>)

Under that, check just the boxes of the fields which you wish to include in the new beneficiary accounts. It's not recommended to select Select All, as that will generate a number of custom attributes which will not likely be useful on the Sempo platform.

![](<../.gitbook/assets/image (38).png>)

Uncheck "Include hyperlink to submission details?" and ensure "Include text summary?" and "Embed binary fields?" remain unchecked.&#x20;

If there is data in the form already which you wish to retroactively add to the Sempo platform, check the "Publish existing data?" box.

Hit the Save button, and now you're finished! Your form is now configured to push data to the Sempo platform!&#x20;

