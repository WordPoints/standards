# Philosophies

This document outlines the development philosophies of the WordPoints organization.

In addition to this document, it is recommended that you also understand [WordPress's
development philosophies](https://make.wordpress.org/core/handbook/our-philosophies/).
WordPoints follows these, except as noted otherwise below.

## Backward Compatibility With Other Libraries

Libraries MAY contain code whose sole purpose is to maintain backward compatibility
with older versions of other libraries (e.g., WordPress). However, libraries SHALL
NOT contain such compatibility code for versions of libraries which are no longer
actively maintained with security updates (e.g., WordPress 3.6).

## Escaping

Everything must be escaped immediately before output/use. Period. [A great read on this
topic](https://vip.wordpress.com/2014/06/20/the-importance-of-escaping-all-the-things/).
