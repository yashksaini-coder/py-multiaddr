History
=======

.. towncrier release notes start

py-multiaddr v0.3.0 (2026-11-22)
--------------------------------

Bugfixes
~~~~~~~~

- Fixed an issue where decapsulate produced incorrect results for repeated protocols and substring collisions. (`#109 <https://github.com/multiformats/py-multiaddr/issues/109>`__)
- Add validation to Multiaddr initialization from bytes to reject invalid sequences immediately (`#110 <https://github.com/multiformats/py-multiaddr/issues/110>`__)
- Fix `string_iter` to correctly handle unix paths and other path protocols by consuming remaining components (`#112 <https://github.com/multiformats/py-multiaddr/issues/112>`__)
- Improve WireGuard codec error messages and align validation with the certhash pattern. (`#130 <https://github.com/multiformats/py-multiaddr/issues/130>`__)
- Fix ruff RUF043 in wg tests and Sphinx docstring warning so ``make pr`` / ``make docs`` pass. (`#145 <https://github.com/multiformats/py-multiaddr/issues/145>`__)
- Fix ``ip6zone`` being decoded as a value-less protocol: ``protocols()``, ``items()``, ``split()`` and binary parsing now handle zone identifiers of any length (e.g. ``en0``, ``wlan0``). (`#147 <https://github.com/multiformats/py-multiaddr/issues/147>`__)


Features
~~~~~~~~

- Add draft WireGuard (``wg``) multiaddr protocol support. Public keys are
  encoded as 32-byte Curve25519 values using multibase base64url (``u`` prefix)
  in textual multiaddrs. Protocol code ``0x01C7`` is provisional until
  registered in the upstream multicodec table. (`#107 <https://github.com/multiformats/py-multiaddr/issues/107>`__)
- Add ``dial_args()`` to convert thin-waist and unix multiaddrs to socket-ready strings. (`#114 <https://github.com/multiformats/py-multiaddr/issues/114>`__)
- Add ``from_net_addr()`` / ``to_net_addr()`` for socket address tuple conversion. (`#115 <https://github.com/multiformats/py-multiaddr/issues/115>`__)
- Add IP classification helpers on ``Multiaddr`` objects (``is_ip_loopback``, ``is_public_addr``, ``is_private_addr``, and related predicates). (`#116 <https://github.com/multiformats/py-multiaddr/issues/116>`__)
- Add ``Filters`` / ``Action`` for accept/deny IP filtering (go-multiaddr parity). (`#117 <https://github.com/multiformats/py-multiaddr/issues/117>`__)
- Add a command-line interface to decode multiaddrs into structured JSON. (`#119 <https://github.com/multiformats/py-multiaddr/issues/119>`__)
- Export commonly used symbols directly from ``multiaddr`` package root. (`#121 <https://github.com/multiformats/py-multiaddr/issues/121>`__)
- Add ``interface_multiaddrs()`` to return local interface addresses as Multiaddr objects. (`#122 <https://github.com/multiformats/py-multiaddr/issues/122>`__)


Internal Changes - for py-multiaddr Contributors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Removed leftover debug logging from multiaddr string/bytes transforms. (`#111 <https://github.com/multiformats/py-multiaddr/issues/111>`__)
- Add ``version.json`` and keep it in sync via bump-my-version (go-multiaddr parity). (`#118 <https://github.com/multiformats/py-multiaddr/issues/118>`__)
- Add an opt-in pytest-benchmark suite for core multiaddr hot paths (``make bench``). (`#120 <https://github.com/multiformats/py-multiaddr/issues/120>`__)
- Fixed Windows CI so each tox matrix job runs only its intended environment instead of the full envlist. (`#134 <https://github.com/multiformats/py-multiaddr/issues/134>`__)
- Pin ``pyrefly==1.2.0`` in the ``dev`` extra so lint CI does not break when newer pyrefly releases add stricter rules. (`#149 <https://github.com/multiformats/py-multiaddr/issues/149>`__)


Miscellaneous Changes
~~~~~~~~~~~~~~~~~~~~~

- `#151 <https://github.com/multiformats/py-multiaddr/issues/151>`__


Performance Improvements
~~~~~~~~~~~~~~~~~~~~~~~~

- Cache the codec object on ``Protocol`` so ``size`` and ``path`` avoid repeated lookups. (`#113 <https://github.com/multiformats/py-multiaddr/issues/113>`__)


py-multiaddr v0.2.0 (2026-03-17)
--------------------------------

Features
~~~~~~~~

- Add resolver utility functions ported from go-multiaddr-dns: ``matches()``, ``resolve_all()``, ``is_fqdn()``, ``fqdn()``, ``addr_len()``, and ``offset_addr()``. These utilities support DNS-based multiaddr resolution workflows including iterative resolution and FQDN handling. (`#101 <https://github.com/multiformats/py-multiaddr/issues/101>`__)


Internal Changes - for py-multiaddr Contributors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Updated the tox GitHub Actions workflow so lint runs only once on Linux with
  Python 3.10, while core tests continue to run across all configured Python
  versions. (`#104 <https://github.com/multiformats/py-multiaddr/issues/104>`__)
- Aligned local tox defaults with CI by running lint only in ``py310-lint``,
  while keeping core test environments for all configured Python versions. (`#106 <https://github.com/multiformats/py-multiaddr/issues/106>`__)


Removals
~~~~~~~~

- Removed the module-level ``to_bytes`` and ``to_string`` helpers from ``multiaddr.codecs.domain``.
  Domain codec behavior remains available through ``multiaddr.codecs.domain.Codec``. (`#100 <https://github.com/multiformats/py-multiaddr/issues/100>`__)


py-multiaddr v0.1.1 (2025-12-07)
--------------------------------

Bugfixes
~~~~~~~~

- Fixed validation for tag-only protocols (protocols that do not accept values).
  Tag-only protocols like ``http``, ``https``, ``tls``, ``noise``, ``webrtc``, etc.
  now correctly reject invalid value assignments via both ``/tag/value`` and
  ``/tag=value`` syntax, raising clear error messages that do not include the
  invalid value. (`#98 <https://github.com/multiformats/py-multiaddr/issues/98>`__)


py-multiaddr v0.1.0 (2025-10-27)
--------------------------------

Features
~~~~~~~~

- Added the following protocols in reference with go-multiaddr

  - SNI: 0x01C1
  - NOISE: 0x01C6
  - CERTHASH:
  - WEBRTC:
  - WEBRTC-DIRECT: (`#181 <https://github.com/multiformats/py-multiaddr/issues/181>`__)


py-multiaddr v0.0.12 (2025-10-21)
---------------------------------

Features
~~~~~~~~

- Added the http-path protocol in reference with go-multiaddr. (`#94 <https://github.com/multiformats/py-multiaddr/issues/94>`__)
- Added ipcidr protocol support to py-multiaddr

  - Implements protocol code 43 (0x2B) for CIDR notation support
  - Full compatibility with Go multiaddr implementation
  - Comprehensive test coverage including edge cases (`#95 <https://github.com/multiformats/py-multiaddr/issues/95>`__)
- Added garlic32 and garlic64 protocol support to py-multiaddr

  - Implements protocol code 446 and 447.
  - Full compatibility with Go multiaddr implementation
  - Comprehensive test coverage including edge cases
  - Complete documentation and examples in examples/garlic/garlic_examples.py
  - Integration with multiaddr documentation system (`#96 <https://github.com/multiformats/py-multiaddr/issues/96>`__)


py-multiaddr v0.0.11 (2025-09-15)
---------------------------------

Improved Documentation
~~~~~~~~~~~~~~~~~~~~~~

- Adds example of DNS address resolution. (`#75 <https://github.com/multiformats/py-multiaddr/issues/75>`__)


Features
~~~~~~~~

- Added support for CIDv1 format and improved sequence protocol handling with enhanced indexing and slicing operations. (`#65 <https://github.com/multiformats/py-multiaddr/issues/65>`__)
- Add quic tests. new quic example (`#66 <https://github.com/multiformats/py-multiaddr/issues/66>`__)
- Adds DNSADDR protocol support. (`#68 <https://github.com/multiformats/py-multiaddr/issues/68>`__)
- Add thin waist address validation (`#72 <https://github.com/multiformats/py-multiaddr/issues/72>`__)
- Adds support for p2p-circuit addresses. (`#74 <https://github.com/multiformats/py-multiaddr/issues/74>`__)
- Added full support for dnsaddr protocol and dns4 and dns6 as well (`#80 <https://github.com/multiformats/py-multiaddr/issues/80>`__)
- Integrated the memory protocol, in reference with go-libp2p (`#92 <https://github.com/multiformats/py-multiaddr/issues/92>`__)


Internal Changes - for py-multiaddr Contributors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Enhanced type safety with comprehensive type hints, improved validation, and expanded test coverage for better code reliability and maintainability. (`#65 <https://github.com/multiformats/py-multiaddr/issues/65>`__)
- Added full tests and doc. All typecheck passes (`#80 <https://github.com/multiformats/py-multiaddr/issues/80>`__)
- Drop python3.9 and run py-upgrade, set up CI, add readthedocs config, updates to Makefile (`#85 <https://github.com/multiformats/py-multiaddr/issues/85>`__)


0.0.10 (2025-6-18)
------------------

* Fix Type Issues and add strict type checks using Ruff & Pyright
* Spec updates, Python 3.4- unsupport & custom registries by @ntninja in #59
* add quic-v1 protocol by @justheuristic in #63
* Fix/typecheck by @acul71 in #65
* chore: rm local pyrightconfig.json by @arcinston in #70

0.0.9 (2019-12-23)
------------------

* Add Multiaddr.__hash__ method for hashable multiaddrs
* Add onion3 address support
* Fix broken reST and links in documentation
* Remove emoji from README.rst

0.0.7 (2019-5-8)
----------------

* include subpackage
* refactor util and codec

0.0.5 (2019-5-7)
----------------

* unhexilified bytes
* new exceptions
* miscellaneous improvements [via alexander255_ `#42`_]

.. _alexander255: https://github.com/alexander255
.. _`#42`: https://github.com/multiformats/py-multiaddr/pull/42

0.0.2 (2016-5-4)
----------------

* Fix a bug in decapsulate that threw an IndexError instead of a copy of the
  Multiaddr when the original multiaddr does not contain the multiaddr to
  decapsulate. [via fredthomsen_ `#9`_]
* Increase test coverage [via fredthomsen_ `#9`_]

.. _fredthomsen: https://github.com/fredthomsen
.. _`#9`: https://github.com/multiformats/py-multiaddr/pull/9

0.0.1 (2016-1-22)
------------------

* First release on PyPI.
