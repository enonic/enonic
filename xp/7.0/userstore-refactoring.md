# User store / ID Provider refactoring

The concept of "User store" and "ID Provider" will change in 7.0.

- What was known as a "User store" is now an "ID Provider".
- What was known as a "Associate an ID Provider to a User store" is now "Associate an application to an ID Provider" (similar to application to site).


## Step1: Refactoring

This epic is about refactoring the code, the APIs to adapt to these changes.

- XP
  - Rename Java classes and fields
  - Adapt messages
  - Adapt the JaxRs API
  - Adapt the JS libraries (Auth and Portal)
- XP App (Content Studio, Users, Application, Standard ID Provider)
  - Adapt to the changes made in XP
  - Rename Java classes and fields
  - Rename TS/JS classes and fields
  - Adapt messages
  
Note:
  Do not touch PrincipalPropertyNames.USER_STORE_KEY
  Do not touch the Virtual Host config
  
## Step2: Data refactoring 
- PrincipalPropertyNames.USER_STORE_KEY
- Dump migration  
  
## Step3: Enable ID Providers for a VHOST Mapping

Modify VHost configuration

    mapping.intranet.host = enonic.com
    mapping.intranet.source = /
    mapping.intranet.target = /portal/master/enonic.com
    mapping.intranet.idProvider.enonic = default
    mapping.intranet.idProvider.enonic.aProperty = aValue
    mapping.intranet.idProvider.system = enabled
    mapping.intranet.idProvider.system.aProperty = anotherValue

The ID Provider controllers should only be called if they are enabled
