UAE Bus Transportation Providers: Documentation & API Guide
===========================================================

In the UAE, public transportation is managed at the emirate level, meaning each major city has its own dedicated authority. While they all provide high-quality, air-conditioned bus services, they differ in their geographic focus, payment systems, and additional transport modes (like metros or marine transport).

Here is a breakdown of the three providers:
  
1. Executive Summary
-------------------

The United Arab Emirates utilizes a decentralized transport model where each Emirate manages its own transit authority. This document highlights **RTA Dubai**, **AD Mobility**, and **RAKTA**, distinguishing their operations and providing a high-level technical overview of their available APIs.

2. Provider Profiles
-------------------

+------------+------------------+-----------------+--------------------------------------------------------------+
| Provider   | Emirate          | Payment System  | Key Differentiator                                           |
+============+==================+=================+==============================================================+
| RTA Dubai  | Dubai            | **nol**         | Highly integrated with Metro/Tram; high-tech smart shelters. |
+------------+------------------+-----------------+--------------------------------------------------------------+
| AD Mobility| Abu Dhabi        | **Hafilat**     | Extensive regional coverage and focus on autonomous ART.     |
+------------+------------------+-----------------+--------------------------------------------------------------+
| RAKTA      | Ras Al Khaimah   | **E-Saqr**      | Focus on inter-emirate and international (Oman) routes.      |
+------------+------------------+-----------------+--------------------------------------------------------------+

RTA Dubai
~~~~~~~~~

The Roads and Transport Authority (RTA) in Dubai manages the most complex public transport network in the UAE, including the driverless Dubai Metro. Bus services primarily act as feeder routes to Metro stations, ensuring seamless last-mile connectivity.

AD Mobility
~~~~~~~~~~~

Abu Dhabi Mobility (formerly ITC) oversees transport across the capital’s vast geography. The authority emphasizes on-demand bus services in suburban zones and is actively deploying the Autonomous Rapid Transit (ART) system.

RAKTA
~~~~~

Ras Al Khaimah Transport Authority serves as a mobility gateway for the northern emirates. Its operations prioritize tourism-friendly routes and long-distance inter-emirate travel.

3. API Documentation (Simple Reference)
--------------------------------------

Most UAE transport data is accessed via the **Dubai Pulse** portal or the **UAE API Marketplace**. Below are simplified API references intended for developers.

A. RTA Dubai (via Dubai Pulse)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dubai provides REST APIs for real-time bus routes and schedules.

- **Endpoint:** ``https://api.dubaipulse.gov.ae/rta/bus_routes``
- **Method:** ``GET``
- **Authentication:** Bearer Token (OAuth2)

Example Request::

  curl -X GET "https://api.dubaipulse.gov.ae/rta/bus_routes?routeId=F11" \
       -H "Authorization: Bearer YOUR_ACCESS_TOKEN"

Response (JSON)::

  {
    "route": "F11",
    "origin": "Satwa Bus Station",
    "destination": "Financial Centre Metro",
    "status": "Active"
  }

B. AD Mobility (via Darb / TAMM)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Abu Dhabi provides **Darb** services for journey planning and mobility data.

- **Endpoint:** ``https://api.itc.gov.ae/transport/v1/bus/stops``
- **Method:** ``GET``
- **Key Parameters:** ``emirate_zone`` (e.g., Abu Dhabi, Al Ain)

Example Request::

  fetch('https://api.itc.gov.ae/transport/v1/bus/stops?zone=city')
    .then(response => response.json())
    .then(data => console.log(data));

C. RAKTA (via Sayr App Integration)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

RAKTA primarily exposes public transport data using **GTFS (General Transit Feed Specification)**.

- **Data Format:** GTFS Static / GTFS Realtime
- **Access:** Request via the RAKTA Open Data Portal

Sample ``routes.txt`` entry::

  route_id,agency_id,route_short_name,route_long_name,route_type
  RAK_DXB,RAKTA,Intercity,RAK to Dubai Union,3

4. Technical Distinctions
------------------------

1. **Data Format**
   - RTA Dubai emphasizes **JSON/REST** APIs for real-time applications.
   - AD Mobility and RAKTA rely heavily on **GTFS** for compatibility with global platforms such as Google Maps and Apple Maps.

2. **Developer Access**
   - RTA integrations require registration via the **Dubai Pulse** developer portal.
   - AD Mobility APIs are commonly provisioned through the **TAMM** (Abu Dhabi Government) ecosystem.

.. toctree::
   :maxdepth: 2

   style-guide
