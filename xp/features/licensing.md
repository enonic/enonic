# License Validation System

## Introduction
There is a need for a licensing system so we can restrict the usage of certain apps to premium customers.

The system should check that the user has a valid license before they can use the application, or certain features in the application.

The system should be as usable as possible and not get in the way, for the customers that have paid for the product.

No licensing system is 100% foolproof, the binary code can always be modified to remove the license validation checks.

## Proposal
Generate licenses using public-key crypto. The license is a data file (e.g. JSON) that will be encrypted using a private key. The application contains the public key, which can be used to validate a license.

The private key is needed to generate the licenses, it should be kept in a safe place. The public key is used to validate, and can be inside the application.

### License
A license is an object with some fixed properties, and possibly some optional custom properties.
- Organization
- Name
- Issue date
- Expire date
- Custom properties depending on the app (key/value)

The license can be serialized as JSON, encrypted using RSA, and base64-encoded. Then it can be easily stored in a file, or in a Node Repo.

### Components:
Some applications and libraries need to be created to facilitate the license system for the users and application developers.

* License-generator application
   * Generates a key-pair for each application that requires license validation. 
   * The public key will be included in the application bundle (.jar)
   * Generates a user license based on the key-pair. This license can be sent to the customer, as a file.
* License-library for validation
   * It will be used in applications
   * API functions to check if a valid license is present, and to obtain info from the license (name, organization, expiry date,...)
* XP API for license installation/validation
   * Not sure if this is really needed?

### Generate license
To generate a license, first we need to generate a key-pair for the application.

The application developer will receive a public and a private key.

The public key should be included in his application.

The private key can be used, together with the customer details, to generate a license.

Each of these is stored in a separate file:
- private key
- public key
- license

### Install license

#### How does a user enter the license?
Some possibilities:
- Copy the file in $XP_home/licenses/
- Use UI in Applications app

#### Where to store the license?
Some possibilities:
- Node repo
- Filesystem: $XP_home/config/ or $XP_home/licenses/

### Validate license
The application decides when to validate the license and what license info to use or show. This is done programatically, from a JS controller (or Java) by calling functions from the License-lib.

The license-lib should take care of finding the license (in filesystem or repo, depending of what is decided), and validate it using the public key included in the app (on a fixed path, e.g. resources/license.key).

The lib should provide some utility functions:
- ```isLicenseValid()```
- ```getLicenseDetails()```
- ```getLicenseName()```
- ```getLicenseProperty('nodeCount')```

It is up to the application developer to react to an invalid/missing license, by blocking requests, showing warning messages or other ways.

### Questions and issues
- Do we need to make the License API part of XP? The api does not need to be in XP, since the validation is done programmatically in the app by calling license api methods. It could just be a separate library. That would mean that the lib code needs not be open source.
