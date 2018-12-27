# User store / ID Provider refactoring

The concept of "User store" and "ID Provider" will change in 7.0.
This epic is about refactoring the code, the APIs and the data to adapt to these changes.

- What was known as a "User store" is now an "ID Provider".
- What was known as a "Associate an ID Provider to a User store" is now "Associate an application to an ID Provider" (similar to application to site).


XP
  Rename Java classes and fields
  Adapt messages
  Adapt the JaxRs API
  Adapt the JS libraries (Auth and Portal)
  Data: PrincipalPropertyNames.USER_STORE_KEY
App Users
  Adapt to the changes made in XP
  Rename Java classes and fields
  Rename TS/JS classes and fields
  Adapt messages
  Adapt the App Users auth JS libraryJS library
Standard ID Provider
  Adapt to the changes made in XP
  Rename Java classes and fields
  Rename TS/JS classes and fields
