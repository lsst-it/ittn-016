:tocdepth: 3

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

Technical Solution Overview
===========================

Data Gathering
--------------

As of early 2017, the Wi-Fi infrastructure for LSST in Chile implemented back then by the IT North group, was comprised of a group of domestic-grade standalone APs with a cluster configuration that allowed authentication to a unique local network using the Active Directory (AD) credentials for each LSST user. The coverage was limited to the old NOAO building where LSST had several offices assigned, and the coverage in Cerro Pachon was provided by NOAO's CTIO group CISS.

CISS's approach to Wi-Fi networks was different as the one implemented by LSST in La Serena, using WPA2 PSKs shared across the staff at the summit, both LSST staff and contractors. The infrastructure used for this was suboptimal as fibers and UTP cables were installed more than 10 years ago and several incidents happened during a working month due to this fact. The Wi-Fi network back then was not connected to the LSST network at the base, and several firewall rules had to be modified by CISS in their Pachon and La Serena firewalls, plus on the LSST firewall for some key communications to happen, e.g. the EarthCam connections.

As the LSST telescope building and the new base facilities are ready, the following summary requirements must be fulfilled by the Wi-Fi infrastructure to be implemented:

1. Due to the high density of APs to cover the telescope building and base facilities, centralized controller-based management is necessary instead of a standalone approach.
2. The chosen AP models must suffice the physical location of installation, which can be indoor office areas, indoor industrial areas, outdoor semi-enclosed areas, or outdoor areas.
3. The solution must allow flexibility to authenticate users with WPA2-PSK, captive portals (open authentication), 802.1x, or WPA2 enterprise, at least. Using internal or external authentication sources, mainly LDAP-based.
4. The solution must allow for multiple networks or SSIDs, associated with different virtual local area networks (VLANs) for differentiated levels of access, including but not limited to LSST staff, contractors, guests (including the potential implementation of Eduroam) and AURA collaborators.
5. The solution must be able to manually set the channels, power budget, frequency of operations in the case of dual-band antennas, offered data rates, and in general, all the key client-facing parameters necessary to control coverage (primary and secondary) and roaming, for Wi-Fi 4 and Wi-Fi 5 at least.
6. The solution must be able to implement local mesh networks for point to point connections of control network systems such as the main LSST dome and the Auxiliary Telescope dome hardware.
7. The solution must be able to provide basic statistics for APs and authenticated clients, including but not limited to: authentication timestamp, mac addresses, data rate and spatial streams used by the client, signal level or RSSI, signal-to-noise ratios (SNR), interference between overlapping channels and non-IEEE 802.11 sources of interference.
8. The solution must be able to split Wi-Fi 4 and Wi-FI 5 in different SSIDs, regardless of how good the band steering capabilities the vendor claims to provide. In the same line, the APs must be able to set its transmission power for Wi-Fi 4 and Wi-Fi 5 antennas independently and any Radio Resource Management (RMM) feature must not be enforced.
9. The solution must allow us to use the local regulatory domain for Chile and allow us to select the specific channels available in such a domain to be used for Wi-Fi 4 and Wi-Fi 5.
10. The chosen APs must be able to handle its local data plane and have a survival mode in case they lose the control plane (the controller itself). Redundancy of the control plane between sites is mandatory. Redundancy of the control plane within the site is a "nice to have" if there's a use-case for a mission-critical application, and if budget allows.

Chosen Solution
---------------

The decision rationale was a technical analysis of the project requirements by several vendors and distributors held in the 2015/2016 timeframe by the Tiger Team, out of which Cisco Systems was the chosen vendor for all the LAN network infrastructure, including Wi-Fi, from which its Wireless Lan Controller (WLC) and Lightweight Access Points (AP) ecosystem was the specific technical solution chosen for the project.

On a high-level, the Cisco WLC solution provides central management for all the APs in the network, including wireless settings such as channels, power budget, interference threshold, user authentication, etc... This is implemented by loading a lightweight version of the AireOS software on the APs, which connects back to the WLC using the Control and Provisioning for Wireless Access Points (CAPWAP) protocol. There are different operating modes for the chosen solution in regards to how the APs forward data and control traffic, both with pros and cons; this document will expand on this matter in section 3.5.

.. figure:: /_static/flexconnect.jpg
    :name: APs in Flexconnect mode
    :width: 550 px

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
