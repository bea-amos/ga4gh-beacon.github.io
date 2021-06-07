---
title: '[H—>O] Beacon Handover for Data Delivery'
date: 2018-10-18
layout: default
author: "@mbaudis"
permalink: /roadmap/handover.html
excerpt_separator: <!--more-->
www_link:
category:
  - beaconv2
tags:
  - specification
  - development
  - roadmap
---

## {{ page.title }}

While the Beacon response should be restricted to aggregate data (yes/no, counts, frequencies ...), the usage of the protocol could be greatly expanded by providing an access method to data elements matched by a Beacon query.

As part of the mid-term product strategy, the ELIXIR Beacon team is evaluating the use of a "handover" protocol, in which rich data content (e.g. variant data, phenotypic information, low-level sequencing results) can be provided from linked services, initiated through a Beacon query (and possibly additional steps like protocol selection, authentication...). A discussion of the topic can e.g. be found in the Beacon developer area on Github ([issue #114](https://github.com/ga4gh-beacon/specification/issues/114)).

As of 2018-11-13, the __handover__ concept has become part of the [ongoing code development](https://github.com/ga4gh-beacon/specification/pull/230/files).

<figure>
<img src="/assets/img/beacon-query-handover-schema.png" style="width: 520px;" />
  <figcaption style="font-size: 0.8em;">Possible scenario for a Beacon-initiated "handover" data delivery, involving pre- or post- query authentication steps. Importantly, the identification of matching "rich" data elements (e.g. information about biosamples or individuals) happens internally, and only a data access handle is exposed to the Beacon ecosystem.</figcaption>
</figure>

<!--more-->

In the latest version of the __handover__ draft (2018-12-18), handover pointers can now be delivered for the Beacon itself (`beaconHandover`) and datasets (`datasetHandover`). An example of `datasetHandover` use is shown below, from the [Beacon+](http://beacon.progenetix.org) implementation.

```
"datasetAlleleResponses": [
  {
    "datasetHandover": [
      {
        "handoverType": {
          "id": "pgx:handover:biosamplesdata",
          "label": "Biosamples"
        },
        "description": "retrieve data of the biosamples matched by the query",
        "url": "http://beacon.progenetix.org/beaconplus-server/beacondeliver.cgi?do=biosamplesdata&accessid=5327fe14-0375-11e9-87ab-f392226922dd"
      },
      {
        "url": "http://beacon.progenetix.org/beaconplus-server/beacondeliver.cgi?do=individualsdata&accessid=53283c62-0375-11e9-87ab-f0c3824efc45",
        "description": "retrieve data of the individuals matched by the query",
        "handoverType": {
          "label": "Individuals",
          "id": "pgx:handover:individualsdata"
        }
      },
      {
        "description": "retrieve data of the variants matched by the query",
        "url": "http://beacon.progenetix.org/beaconplus-server/beacondeliver.cgi?do=variantsdata&accessid=53273f2d-0375-11e9-87ab-958a9c7ac1d4",
        "handoverType": {
          "id": "pgx:handover:variantsdata",
          "label": "Variants"
        }
      }
    ],
 ...
```
