# User store / ID Provider refactoring

## Epic1: Renaming

The concept of "User store" and "ID Provider" will change in 7.0.

- What was known as a "User store" is now an "ID Provider".
- What was known as "Associating an ID Provider to a User store" is now "Associating an application to an ID Provider" (similar to associating an application to site).

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
  - Leave untouched the data (PrincipalPropertyNames.USER_STORE_KEY)
  - Leave untouched the virtual host config
  - In many cases, "ID Provider" was used correctly and should not be changed.
For example, the ID Provider controller should remain under /idprovider/idprovider.js and the ID Provider URL (*/_/idprovider/<userstore>/*) should be left untouched.

## Feature2: Data refactoring 
- PrincipalPropertyNames.USER_STORE_KEY
- Dump migration  
  
## Feature3: Enable ID Providers for a VHOST Mapping

Modify VHost configuration

    mapping.intranet.host = enonic.com
    mapping.intranet.source = /
    mapping.intranet.target = /portal/master/enonic.com
    mapping.intranet.idProvider.enonic = default
    mapping.intranet.idProvider.enonic.aProperty = aValue
    mapping.intranet.idProvider.system = enabled
    mapping.intranet.idProvider.system.aProperty = anotherValue

The ID Provider controllers should only be called if they are enabled
