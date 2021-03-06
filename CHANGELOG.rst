Changelog
=========

0.5 - `master`
~~~~~~~~~~~~~~

.. note:: This version is not yet released and is under active development


0.4 - ``
~~~~~~~~

There have been quite a few issues closed in this release. Some notables:

* Closed `#284 <https://github.com/Netflix/lemur/issues/284>`_ - Created new models for `Endpoints` created associated
AWS ELB endpoint tracking code. This was the major stated goal of this milestone and should serve as the basis for
future enhancements of Lemur's certificate 'deployment' capabilities.

* Closed `#334 <https://github.com/Netflix/lemur/issues/334>`_ - Lemur not has the ability
to restrict certificate expiration dates to weekdays.

Several fixes/tweaks to Lemurs python3 support (thanks chadhendrie!)

This will most likely be the last release to support python2.7 moving Lemur to target python3 exclusively. Please comment
on issue #340 if this negatively affects your usage of Lemur.

Upgrading
---------

See the full list of issues closed in `0.4 <https://github.com/Netflix/lemur/milestone/3>`_.

.. note:: This release will need a slight migration change. Please follow the `documentation <https://lemur.readthedocs.io/en/latest/administration.html#upgrading-lemur>`_ to upgrade Lemur.


0.3.0 - `2016-06-06`
~~~~~~~~~~~~~~~~~~~~

This is quite a large upgrade, it is highly advised you backup your database before attempting to upgrade as this release
requires the migration of database structure as well as data.


Upgrading
---------

Please follow the `documentation <https://lemur.readthedocs.io/en/latest/administration.html#upgrading-lemur>`_ to upgrade Lemur.


Source Plugin Owners
--------------------

The dictionary returned from a source plugin has changed keys from `public_certificate` to `body` and `intermediate_certificate` to chain.


Issuer Plugin Owners
--------------------

This release may break your plugins, the keys in `issuer_options` have been changed from `camelCase` to `under_score`.
This change was made to break a undue reliance on downstream options maintains a more pythonic naming convention. Renaming
these keys should be fairly trivial, additionally pull requests have been submitted to affected plugins to help ease the transition.

.. note:: This change only affects issuer plugins and does not affect any other types of plugins.


* Closed `#63 <https://github.com/Netflix/lemur/issues/63>`_ - Validates all endpoints with Marshmallow schemas, this allows for
    stricter input validation and better error messages when validation fails.
* Closed `#146 <https://github.com/Netflix/lemur/issues/146>`_ - Moved authority type to first pane of authority creation wizard.
* Closed `#147 <https://github.com/Netflix/lemur/issues/147>`_ - Added and refactored the relationship between authorities and their
    root certificates. Displays the certificates (and chains) next the the authority in question.
* Closed `#199 <https://github.com/Netflix/lemur/issues/199>`_ - Ensures that the dates submitted to Lemur during authority and
    certificate creation are actually dates.
* Closed `#230 <https://github.com/Netflix/lemur/issues/230>`_ - Migrated authority dropdown to a ui-select based dropdown, this
    should be easier to determine what authorities are available and when an authority has actually been selected.
* Closed `#254 <https://github.com/Netflix/lemur/issues/254>`_ - Forces certificate names to be generally unique. If a certificate name
    (generated or otherwise) is found to be a duplicate we increment by appending a counter.
* Closed `#254 <https://github.com/Netflix/lemur/issues/275>`_ - Switched to using Fernet generated passphrases for exported items.
    These are more sounds that pseudo random passphrases generated before and have the nice property of being in base64.
* Closed `#278 <https://github.com/Netflix/lemur/issues/278>`_ - Added ability to specify a custom name to certificate creation, previously
    this was only available in the certificate import wizard.
* Closed `#281 <https://github.com/Netflix/lemur/issues/281>`_ - Fixed an issue where notifications could not be removed from a certificate
    via the UI.
* Closed `#289 <https://github.com/Netflix/lemur/issues/289>`_ - Fixed and issue where intermediates were not being properly exported.
* Closed `#315 <https://github.com/Netflix/lemur/issues/315>`_ - Made how roles are associated with certificates and authorities much more
    explict, including adding the ability to add roles directly to certificates and authorities on creation.



0.2.2 - 2016-02-05
~~~~~~~~~~~~~~~~~~

* Closed `#234 <https://github.com/Netflix/lemur/issues/234>`_ - Allows export plugins to define whether they need
    private key material (default is True)
* Closed `#231 <https://github.com/Netflix/lemur/issues/231>`_ - Authorities were not respecting 'owning' roles and their
    users
* Closed `#228 <https://github.com/Netflix/lemur/issues/228>`_ - Fixed documentation with correct filter values
* Closed `#226 <https://github.com/Netflix/lemur/issues/226>`_ - Fixes issue were `import_certificate` was requiring
    replacement certificates to be specified
* Closed `#224 <https://github.com/Netflix/lemur/issues/224>`_ - Fixed an issue where NPM might not be globally available (thanks AlexClineBB!)
* Closed `#221 <https://github.com/Netflix/lemur/issues/234>`_ - Fixes several reported issues where older migration scripts were
    missing tables, this change removes pre 0.2 migration scripts
* Closed `#218 <https://github.com/Netflix/lemur/issues/234>`_ - Fixed an issue where export passphrases would not validate


0.2.1 - 2015-12-14
~~~~~~~~~~~~~~~~~~

* Fixed bug with search not refreshing values
* Cleaned up documentation, including working supervisor example (thanks rpicard!)
* Closed #165 - Fixed an issue with email templates
* Closed #188 - Added ability to submit third party CSR
* Closed #176 - Java-export should allow user to specify truststore/keystore
* Closed #176 - Extended support for exporting certificate in P12 format


0.2.0 - 2015-12-02
~~~~~~~~~~~~~~~~~~

* Closed #120 - Error messages not displaying long enough
* Closed #121 - Certificate create form should not be valid until a Certificate Authority object is available
* Closed #122 - Certificate API should allow for the specification of preceding certificates
    You can now target a certificate(s) for replacement. When specified the replaced certificate will be marked as
    'inactive'. This means that there will be no notifications for that certificate.
* Closed #139 - SubCA autogenerated descriptions for their certs are incorrect
* Closed #140 - Permalink does not change with filtering
* Closed #144 - Should be able to search certificates by domains covered, included wildcards
* Closed #165 - Cleaned up expiration notification template
* Closed #160 - Cleaned up quickstart documentation (thanks forkd!)
* Closed #144 - Now able to search by all domains in a given certificate, not just by common name


0.1.5 - 2015-10-26
~~~~~~~~~~~~~~~~~~

* **SECURITY ISSUE**: Switched from use a AES static key to Fernet encryption.
  Affects all versions prior to 0.1.5. If upgrading this will require a data migration.
  see: `Upgrading Lemur <https://lemur.readthedocs.com/adminstration#UpgradingLemur>`_
