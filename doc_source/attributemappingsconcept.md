# Attribute Mappings<a name="attributemappingsconcept"></a>

AWS SSO retrieves user attributes from your connected directory and maps them to AWS SSO user attributes\. These AWS SSO user attribute mappings are also used for generating SAML assertions for your cloud applications\. Each cloud application determines the list of SAML attributes it needs for successful single sign\-on\. 

AWS SSO prefills a set of attributes for you under the **Attribute mappings** tab found on your application's configuration page\. AWS SSO uses these user attributes to populate SAML assertions \(as SAML attributes\) that are sent to the cloud application\. These user attributes are in turn retrieved from your connected directory\. For more information, see [Map Attributes in Your Application to AWS SSO Attributes](mapawsssoattributestoapp.md)\. 

AWS SSO also manages a set of attributes for you under the **Attribute mappings** section of your connected directory configuration page\. For more information, see [Map Attributes in AWS SSO to Attributes in Your Connected Directory](mapssoattributestocdattributes.md)\.

## Supported Directory Attributes<a name="supporteddirectoryattributes"></a>

The following table provides the full list of connected directory attributes that are supported and which can be mapped to user attributes in AWS SSO\. 


****  

| Supported attributes in your connected directory | 
| --- | 
| $\{dir:email\} | 
| $\{dir:displayname\} | 
| $\{dir:distinguishedName\} | 
| $\{dir:firstname\} | 
| $\{dir:guid\} | 
| $\{dir:initials\} | 
| $\{dir:lastname\} | 
| $\{dir:proxyAddresses\} | 
| $\{dir:proxyAddresses:smtp\} | 
| $\{dir:proxyAddresses:SMTP\} | 
| $\{dir:windowsUpn\} | 

You can specify any combination of supported connected directory attributes to map to a single attribute in AWS SSO\. For example, you could choose the “preferredUsername” attribute under the **User attribute in AWS SSO** column and then map it to either $\{dir:displayname\}, or $\{dir:lastname\}$\{dir:firstname \}, or any single supported attribute, or any arbitrary combination of supported attributes\.

## Supported AWS SSO Attributes<a name="supportedssoattributes"></a>

The following table provides the full list of AWS SSO attributes that are supported and which can be mapped to user attributes in your connected directory\. Later, when you set up your application attribute mappings you will be able to use these same AWS SSO attributes to map to actual attributes used by that application\.


****  

| Supported attributes in AWS SSO | 
| --- | 
| $\{user:AD\_GUID\} | 
| $\{user:email\} | 
| $\{user:familyName\} | 
| $\{user:firstName\} | 
| $\{user:middleName\} | 
| $\{user:name\} | 
| $\{user:preferredUsername\} | 
| $\{user:subject\} | 

## Default Mappings<a name="defaultattributemappings"></a>

The following table shows the default mappings for user attributes in AWS SSO to the user attributes in your connected directory\. At this time, AWS SSO only supports the list of attributes shown in the **User attribute in AWS SSO** column\. 


****  

| User attribute in AWS SSO  | Maps to this attribute in your connected directory | 
| --- | --- | 
| AD\_GUID | $\{dir:guid\} | 
| email | $\{dir:windowsUpn\} | 
| familyName | $\{dir:lastname\} | 
| givenName | $\{dir:firstname\} | 
| middleName | $\{dir:initials\} | 
| name | $\{dir:displayname\} | 
| preferredUsername | $\{dir:displayname\} | 
| subject | $\{dir:windowsUpn\} | 

You can change the default mappings or add more attributes to the SAML assertion based on your requirements\. For example, if your cloud application requires the users email in the `User.Email` SAML attribute, and emails are stored in the `windowsUpn` attribute in your connected directory\. To achieve this mapping, you would need to make changes in the following two places in the AWS SSO console:

1. On the **Connected Directory** page, under the **Attribute mappings** section, you would need to map the user attribute **`email`** to the **`${dir:windowsUpn}`** attribute \(in the **Maps to this attribute in your connected directory** column\)

1. On the **Applications** page, choose the application from the table, choose the **Attribute mappings** tab, and then you would need to map the `User.Email` attribute to the **`${user:email}`** attribute \(in the **Maps to this string value or user attribute in AWS SSO** column\)\.

Please note that, you must supply each directory attribute in the form $\{dir:**AttributeName**\}\. For example, the `firstname` attribute in your connected directory becomes `${dir:firstname}`\. It is important that every directory attribute have an actual value assigned\. Attributes missing a value after $\{dir: will cause user sign\-in issues\.