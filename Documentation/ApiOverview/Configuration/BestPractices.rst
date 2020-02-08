.. include:: ../../Includes.txt


============================
Configuration best practices
============================

Site package extension
======================

While you can configure TypoScript and TSconfig in the Backend, it is general good practice
to include all configuration for a site (including TypoScript, TSconfig, rte_ckeditor
configuration, Backend Layouts etc.) in a sitepackage extension.

More information:

* Advantages of site packages, basics:
  `Benjamin Kott: The anatomy of sitepackages <https://de.slideshare.net/benjaminkott/typo3-the-anatomy-of-sitepackages>`__
* Tutorial for writing a site package: :ref:`t3sitepackage:start`
