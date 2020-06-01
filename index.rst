:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. note::

   **This technote is a work in progress.**


Introduction
============

The purpose of this document is to outline the Wi-Fi infrastructure high-level design (HLD) for the LSST summit and base sites. It would recommend an architecture based on the requirements set by the project, especially -but not limited to- the Tiger Team in different ICDs and in the documents mentioned in section 1.4.

The intent of this document is to provide an architecture that fulfills the requirements outlined by the project, keeping in mind current needs but also future growth of the network. The HLD does not delve into low-level details (i.e. configuration files, performance analysis, etc...).

As long as the HLD status is draft, it is susceptible to modifications and additions by the IT group or by the request of other subsystems.

After the acceptance of this document, it may be or not under change control, and regardless of that it is considered a living document that will be updated upon requirements addition or changes, experiences from the deployment and operations process.

Scope
-----
- Deliver a recommended Wi-Fi architecture for the project.
- Deliver enough details to allow for a Low-Level Desing (LLD) document.
- Fulfill the current Wi-Fi needs of the project and allow for future growth.
- This document focuses only on Wi-Fi network requirements for systems directly connected campus and/or control networks in the standard Wi-FI 4 and 5 bands.
- This document DOES NOT cover requirements for parallel Wi-FI mesh networks and any other wireless communication system working in non-IEEE 802.11 bands, including wireless sensors or Bluetooth beacons of any kind.

Assumptions and Caveats
-----------------------
- It is assumed all the project concepts derived from other documents such as those mentioned in section 1.4 and/or the associated ICDs, are correct and remain unchanged.
- It is assumed the reader is familiar with the project Wi-Fi requirements. Furthermore, it is also assumed the reader is familiar with Wi-Fi technologies as defined by the IEEE 802.11 standards and has a basic understanding of networking concepts and the technologies that will be used to fulfill the aforementioned requirements

Related Documents
-----------------
- LSE-78 LSST Observatory Network Design
- LSE-309 Summit to Base ITC Design

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
