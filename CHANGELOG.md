## 25.4 (------)

Bug Fixes:

* Repair "View at..." links in tree view context menus.

## 25.3 (221108)

Enhancements:

* Upgrade `dojo`, `pfsc-moose`, and `socket.io-client`
  ([#2](https://github.com/proofscape/pfsc-ise/pull/2)).

## 25.2 (221101)

Enhancements:

* Upgrade to `pfsc-pdf v3.1.0`.

## 25.1 (221030)

Bug Fixes:

* Reinstate synchronous signalling element. v25.0 inadvertently disrupted
  signalling between PISE and the PBE. This restores it.

## 25.0 (221028)

Features:

* The contents of the "About" dialog are now generated here, at compile time
  ([#1](https://github.com/proofscape/pfsc-ise/pull/1)).

Bug Fixes:

* Repair CSS so "comparison panel" in editor is visible when version on disk
  differs from version in editor.

Breaking Changes:

* In a move to no longer repeat ourselves with JS version numbers, we load JS
  assets in new ways ([#1](https://github.com/proofscape/pfsc-ise/pull/1)).

Requires:

* `pfsc-server >= 0.25.0`
* `pfsc-manage >= 0.25.0`

## 24.0 (221016)

Features:

* Populate the new fields in PDF panel help text, regarding PBE activation.

Breaking Changes:

* Use the `pdfjsURL` from the served state to load `viewer.html` in PDF panels.

Requires:

* `pfsc-server >= 0.24.0`

## 23.3 (220920)

Features:

* Hide User menu when logins are not possible.
