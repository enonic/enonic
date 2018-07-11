# Mustache & Thymeleaf as separate libraries

* Mustache must be a separate library
* Thymeleaf must be a separate library (TBD)

## Requirements

* Mustache is in a separate repository
  * Is documented in AsciiDoc and has its own version 1.0.0
* Thymeleaf is in a separate repository (TBD)
  * Is documented in AsciiDoc doc and has its own version 1.0.0

## Dependencies

None

## To be discussed

* Thymeleaf: Thymeleaf, with its view functions, is not a generic Thymeleaf library but a library tightly coupled to Enonic XP.
  * Proposition: Should be kept in the runtime

## Details

* I supposed in the case of Mustache that the code in *-api modules is an Enonic XP API and should not break between major versions
=> ResourceService may not have breaking changes.
