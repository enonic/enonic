# Modal ID Providers

As an application developer, I want to display an ID Provider, without having to redirect, as a modal dialog with overlay.

## Requirements
* Modifying the userstore ID Prov should affect all applications using the modal ID Provider
* This feature should not break existing behaviour of ID Provider
* This should be available under for admin tools. Current behaviour is that if not in LIVE mode many resources require admin login (incl. Admin tools)
* There should be a mechanism to warn the calling app that the authentication has been successful or failed.
