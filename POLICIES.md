# Policies

This document outlines the development policies of the WordPoints organization.

In addition to this document, it is recommended that you also understand [WordPoints's
development philosophies](PHILOSOPHIES.md).

## Release Cycle

The release cycle of the WordPoints plugin SHALL consist of a period of alpha development,
followed by a beta period. During the alpha period breaking changes may take place in the
code. The beta period SHALL last approximately 1 month. During the final 1-2 weeks of this
beta period, a RC (release candidate) period SHALL be declared. During the RC period, there
SHALL NOT be any breaking changes, unless necessary to fix a critical security issue. 
During the RC period, a string freeze SHALL also be enforced, and no translation string
additions or changes may be made.

## Release Schedule

WordPoints SHALL follow a release schedule coinciding with that of WordPress. Each new
WordPoints version will be released approxiamtely at the same time as a WordPress
release. This is to allow modules to be tested for compatibility with the latest
versions of WordPoints and WordPress simultaneously.

## WordPress Compatibility

Each WordPoints release SHALL be compatible with the version of WordPress whose
release it coincides with, and with the WordPress version preceeding that. For
example, the version of WordPoints released along with WordPress 4.7 would support
WordPress 4.7 and 4.6.
