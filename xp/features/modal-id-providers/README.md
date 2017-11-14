# Modal ID Providers

As an application developer, I want to display an ID Provider, without having to redirect, as a modal dialog with overlay.
As an ID Provider developer, I should be able to return a JS script to be included inside an app

## Requirements
* Modifying the userstore ID Prov should affect all applications using the modal ID Provider
* This feature should not break existing behaviour of ID Provider
* This should be available under for admin tools. Current behaviour is that if not in LIVE mode many resources require admin login (incl. Admin tools)
* There should be a mechanism to warn the calling app that the authentication has been successful or failed.
* All ID Provider modal script must share the same interface

## Examples

![Diagram](diagram.jpg?raw=true)
![Example 1](new-standard-id-provider.001.jpeg?raw=true)
![Example 2](new-standard-id-provider.002.jpeg?raw=true)
![Example 3](new-standard-id-provider.003.jpeg?raw=true)
![Example 4](new-standard-id-provider.004.jpeg?raw=true)

