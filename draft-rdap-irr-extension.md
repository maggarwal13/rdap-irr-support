---

title: "RDAP Extension for Internet Routing Registry (IRR) Objects"
abbrev: "RDAP-IRR"
category: info

docname: draft-rdap-irr-extension-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Operations and Management"
workgroup: Internet Engineering Task Force
keyword:
  - RDAP
  - IRR
  - RPSL
venue:
  group: regext
  type: Working Group
  mail: regext@ietf.org
  arch: https://mailarchive.ietf.org/arch/browse/regext/
  github: maggarwal13/rdap-irr-support
  latest: https://maggarwal13.github.io/rdap-irr-support/draft-rdap-irr-extension.html

author:
  -
    fullname: Mahesh Aggarwal
    organization: RIPE NCC
    email: maggarwal@ripe.net
  -
    fullname: Jasdip Singh
    organization: ARIN
    email: jasdips@arin.net
  -
    fullname: Andy Newton
    organization: ICANN
    email: andy@hxr.us
  -
    fullname: Sasha Romijn
    organization: Reliably Coded
    email: sasha@reliablycoded.nl

normative:
  RFC2622:
  RFC4012:
  RFC5943:
  RFC7480:
  RFC9082:
  RFC9083:

informative:
  RFC6973:
  RFC7481:
  RFC8446:
  BCP195:
  I-D.ietf-grow-rpsl-via:

...

--- abstract

The Registration Data Access Protocol (RDAP) is used by Regional Internet Registries (RIRs) and Domain Name Registries (DNRs) to provide access to their resource registration information.
The core specifications for RDAP defines core object types, but it does not contain objects for Internet Routing Registries (IRRs).
This document is intended to address this gap.

--- middle

# Introduction

The Registration Data Access Protocol (RDAP) {{RFC7480}} is used by Regional Internet Registries (RIRs) and Domain Name Registries (DNRs) to provide access to their resource registration information.
The core specifications for RDAP defines core object types, but it does not contain objects for Internet Routing Registries (IRRs).
This document is intended to address this gap.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

Indentation and whitespace in examples are provided only to illustrate element relationships, and are not a required feature of this specification.

"..." in examples is used as shorthand for elements defined outside of this document, as well as to abbreviate elements that are too long.

To keep the examples short, entities in them only include the "objectClassName", "handle", and "roles" members.

# Lookup Path Segment specification

{{Section 3.1 of RFC9082}} defines the simple lookup path segments for types: "ip", "autnum", "domain", "nameserver", and "entity".

This document aims to extend this to add following path segments:

* "irr0_route" -- Used to identify ROUTE object and associated IP address prefix and the autonomous system (AS) that originates it
* "irr0_routeSet" -- Used to identify route-set object
* "irr0_autnumSet" -- Used to identify as-set object
* "irr0_rtrSet" -- Defines the name of the rtr-set
* "irr0_peeringSet" -- Specifies the name of the peering-set
* "irr0_filterSet" -- Defines the name of the filter

# The Route Object Class

It is the RDAP representation of the RPSL route class defined in {{Section 4 of RFC2622}}

Syntax: `irr0_route/< IP prefix of the interAS route >/< AS that originates the route >`

For example, the following URL would be used to find information describing route object

    https://example.net/irr0_route/192.0.2.0/24/64500

The route object class can contain the following members:

* "objectClassName" -- the string "irr0_route"
* "handle" -- a string representing the registry-unique identifier of the route object
* "route" -- a string representing the address-prefix for which a route is referenced; as per {{Section 4 of RFC2622}}
* "origin" -- a string representing an autonomous system number for which a route is referenced; as per {{Section 4 of RFC2622}}
* "routeVersion" -- a string signifying the ip protocol version of the network: "v4" signifies an route with ipv4 network, and "v6" signifies a route with ipv6 network
* "remarks" -- see {{Section 4.3 of RFC9083}}
* "pingable" -- an array of strings each containing a value as specified in {{Section 2 of RFC5943}}
* "holes" -- an array of strings each containing a value as specified in {{Section 8.1 of RFC2622}}
* "member-of" -- an array of strings, each containing a value as specified in {{Section 5.2 of RFC2622}}
* "inject" -- an array of strings, each containing a value as specified in {{Section 8 of RFC2622}}
* "components" -- a string containing a value as specified in {{Section 8.1 of RFC2622}}
* "aggregateBoundary" -- a string containing a value as specified in {{Section 8.1 of RFC2622}}
* "aggregateMtd" -- a string containing a value as specified in {{Section 8.1 of RFC2622}}
* "exportComps" -- a string containing a value as specified in {{Section 8.1 of RFC2622}}
* "entities" -- an array of entity objects as defined by {{Section 5.1 of RFC9083}}
* "links" -- see {{Section 4.2 of RFC9083}}
* "port43" -- see {{Section 4.7 of RFC9083}}
* "events" -- see {{Section 4.5 of RFC9083}}

The following is an example of the JSON object

~~~ json
{
  "objectClassName": "irr0_route",
  "handle": "192.0.2.0/24AS64500",
  "routeVersion": "v4",
  "origin": "64500",
  "route": "192.0.2.0/24",
  "pingable": [ "192.0.2.1" ],
  "holes": [ "192.0.2.64/26" ],
  "member-of": [ "RS-FOO", "RS-BAR" ],
  "remarks": [
    {
      "description": [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "country": "NL",
  "inject": [
    "upon HAVE-COMPONENTS {192.0.2.0/25, 192.0.2.128/25}"
  ],
  "aggr-mtd": "outbound AS-ANY",
  "aggr-bndry": "AS64500 OR AS64501",
  "export-comps": "{192.0.2.128/26}",
  "components": "{192.0.2.0/24^-}",
  "entities": [
    {
      "objectClassName": "entity",
      "handle": "XXXX",
      "roles": [ "registrant" ]
    }
  ],
  "links": [
    {
      "value": "https://example.net/irr0_route/192.0.2.0/24/64500",
      "rel": "self",
      "href": "https://example.net/irr0_route/192.0.2.0/24/64500",
      "type": "application/rdap+json"
    }
  ],
  "events": [
    {
      "eventAction": "registration",
      "eventDate": "1990-12-31T23:59:59Z"
    },
    {
      "eventAction": "last changed",
      "eventDate": "1991-12-31T23:59:59Z"
    }
  ]
}
~~~

# The SET Object Class

{{Section 5 of RFC2622}} defines SET objects.
This section aims to represent SET classes in RDAP representation.
Support for peering-set, rtr-set and filter-set is optional and may be provided at the discretion of the implementation.

## Route Set Object Class

It is the RDAP representation of the RPSL route-set class defined in {{Section 5.2 of RFC2622}}

Syntax: `irr0_routeSet/< name of the route set >`

For example, the following URL would be used to find information describing route-set object

    https://example.net/irr0_routeSet/RS-FOO

The routeSet object class can contain the following members:

* "objectClassName" -- the string "irr0_routeSet"
* "handle" -- a string representing the registry-unique identifier of the routeSet object.
* "members" -- an array of strings, each containing a value as specified in {{Section 5.2 of RFC2622}}
* "mp-members" -- an array of strings, each containing a value as specified in {{Section 4.2 of RFC4012}}
* "remarks" -- see {{Section 4.3 of RFC9083}}
* "entities" -- an array of entity objects as defined by {{Section 5.1 of RFC9083}}
* "links" -- see {{Section 4.2 of RFC9083}}
* "port43" -- see {{Section 4.7 of RFC9083}}
* "events" -- see {{Section 4.5 of RFC9083}}

The following is an example of a routeSet that might be served by an RIR.

~~~ json
{
  "objectClassName": "irr0_routeSet",
  "handle": "RS-FOO",
  "members": [ "192.0.2.0/24", "RS-BAR" ],
  "mp-members": [ "2001:db8::/32" ],
  "remarks": [
    {
      "description": [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "entities": [
    {
      "objectClassName": "entity",
      "handle": "XXXX",
      "roles": [ "registrant" ]
    }
  ],
  "links": [
    {
      "value": "https://example.net/irr0_routeSet/RS-FOO",
      "rel": "self",
      "href": "https://example.net/irr0_routeSet/RS-FOO",
      "type": "application/rdap+json"
    }
  ],
  "events": [
    {
      "eventAction": "registration",
      "eventDate": "1990-12-31T23:59:59Z"
    },
    {
      "eventAction": "last changed",
      "eventDate": "1991-12-31T23:59:59Z"
    }
  ]
}
~~~

## Autnum Set Object Class

It is the RDAP representation of the RPSL autnum-set class defined in {{Section 5.1 of RFC2622}}

Syntax: `irr0_autnumSet/< name of the as-set >`

For example, the following URL would be used to find information describing autnum-set object

    https://example.net/irr0_autnumSet/AS-FOO

The autnumSet object class can contain the following members:

* "objectClassName" -- the string "irr0_autnumSet"
* "handle" -- a string representing the registry-unique identifier of the autnumSet object.
* "members" -- an array of strings, each containing a value as specified in {{Section 5.1 of RFC2622}}
* "remarks" -- see {{Section 4.3 of RFC9083}}
* "entities" -- an array of entity objects as defined by {{Section 5.1 of RFC9083}}
* "links" -- see {{Section 4.2 of RFC9083}}
* "port43" -- see {{Section 4.7 of RFC9083}}
* "events" -- see {{Section 4.5 of RFC9083}}

The following is an example of an autnumSet that might be served by an RIR.

~~~ json
{
  "objectClassName": "irr0_autnumSet",
  "handle": "AS-FOO",
  "members": [ "AS64501", "AS64502", "AS-BAR" ],
  "remarks": [
    {
      "description": [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "entities": [
    {
      "objectClassName": "entity",
      "handle": "XXXX",
      "roles": [ "registrant" ]
    }
  ],
  "links": [
    {
      "value": "https://example.net/irr0_autnumSet/AS-FOO",
      "rel": "self",
      "href": "https://example.net/irr0_autnumSet/AS-FOO",
      "type": "application/rdap+json"
    }
  ],
  "events": [
    {
      "eventAction": "registration",
      "eventDate": "1990-12-31T23:59:59Z"
    },
    {
      "eventAction": "last changed",
      "eventDate": "1991-12-31T23:59:59Z"
    }
  ]
}
~~~

## RTR Set Object Class

It is the RDAP representation of the RPSL rtr-set class defined in {{Section 5.5 of RFC2622}}

Syntax: `irr0_rtrSet/< name of the router-set >`

For example, the following URL would be used to find information describing rtrSet object

    https://example.net/irr0_rtrSet/RTRS-FOO

The rtrSet set object class can contain the following members:

* "objectClassName" -- the string "irr0_rtrSet"
* "handle" -- a string representing the registry-unique identifier of the rtrSet.
* "members" -- an array of strings, each containing a value as specified in {{Section 5.5 of RFC2622}}
* "mp-members" -- an array of strings, each containing a value as specified in {{Section 4.6 of RFC4012}}
* "remarks" -- see {{Section 4.3 of RFC9083}}
* "entities" -- an array of entity objects as defined by {{Section 5.1 of RFC9083}}
* "links" -- see {{Section 4.2 of RFC9083}}
* "port43" -- see {{Section 4.7 of RFC9083}}
* "events" -- see {{Section 4.5 of RFC9083}}

The following is an example of rtrSet that might be served by an RIR.

~~~ json
{
  "objectClassName": "irr0_rtrSet",
  "handle": "RTRS-FOO",
  "members": [ "rtr1.example.net", "rtr2.example.net" ],
  "mp-members": [ "2001:db8::1" ],
  "remarks": [
    {
      "description": [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "entities": [
    {
      "objectClassName": "entity",
      "handle": "XXXX",
      "roles": [ "registrant" ]
    }
  ],
  "links": [
    {
      "value": "https://example.net/irr0_rtrSet/RTRS-FOO",
      "rel": "self",
      "href": "https://example.net/irr0_rtrSet/RTRS-FOO",
      "type": "application/rdap+json"
    }
  ],
  "events": [
    {
      "eventAction": "registration",
      "eventDate": "1990-12-31T23:59:59Z"
    },
    {
      "eventAction": "last changed",
      "eventDate": "1991-12-31T23:59:59Z"
    }
  ]
}
~~~

## Peering Set Object Class

It is the RDAP representation of the RPSL peering-set class defined in {{Section 5.6 of RFC2622}}

Syntax: `irr0_peeringSet/< name of the peering-set >`

For example, the following URL would be used to find information describing peering-set object

    https://example.net/irr0_peeringSet/PRNG-FOO

The peeringSet object class can contain the following members:

* "objectClassName" -- the string "irr0_peeringSet"
* "handle" -- a string representing the registry-unique identifier of the peeringSet
* "peering" -- an array of strings, each containing a value as specified in {{Section 5.6 of RFC2622}}
* "mp-peering" -- an array of strings, each containing a value as specified in {{Section 4.4 of RFC4012}}
* "remarks" -- see {{Section 4.3 of RFC9083}}
* "entities" -- an array of entity objects as defined by {{Section 5.1 of RFC9083}}
* "links" -- see {{Section 4.2 of RFC9083}}
* "port43" -- see {{Section 4.7 of RFC9083}}
* "events" -- see {{Section 4.5 of RFC9083}}

The following is an example of peeringSet that might be served by an RIR.

~~~ json
{
  "objectClassName": "irr0_peeringSet",
  "handle": "PRNG-FOO",
  "peering": [ "AS64501 at 198.51.100.1" ],
  "mp-peering": [ "AS64502 2001:db8::2 at 2001:db8::1" ],
  "remarks": [
    {
      "description": [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "entities": [
    {
      "objectClassName": "entity",
      "handle": "XXXX",
      "roles": [ "registrant" ]
    }
  ],
  "links": [
    {
      "value": "https://example.net/irr0_peeringSet/PRNG-FOO",
      "rel": "self",
      "href": "https://example.net/irr0_peeringSet/PRNG-FOO",
      "type": "application/rdap+json"
    }
  ],
  "events": [
    {
      "eventAction": "registration",
      "eventDate": "1990-12-31T23:59:59Z"
    },
    {
      "eventAction": "last changed",
      "eventDate": "1991-12-31T23:59:59Z"
    }
  ]
}
~~~

## Filter Set Object Class

It is the RDAP representation of the RPSL filter-set class defined in {{Section 5.4 of RFC2622}}

Syntax: `irr0_filterSet/< name of the filter >`

For example, the following URL would be used to find information describing filter object

    https://example.net/irr0_filterSet/FLTR-FOO

The filterSet object class can contain the following members:

* "objectClassName" -- the string "irr0_filterSet"
* "handle" -- a string representing the registry-unique identifier of the filterSet
* "filter" -- an array of strings each defines the set's policy filter as per {{Section 5.4 of RFC2622}}
* "mp-filter" -- an array of strings, each containing a value as specified in {{Section 4.3 of RFC4012}}
* "remarks" -- see {{Section 4.3 of RFC9083}}
* "entities" -- an array of entity objects as defined by {{Section 5.1 of RFC9083}}
* "links" -- see {{Section 4.2 of RFC9083}}
* "port43" -- see {{Section 4.7 of RFC9083}}
* "events" -- see {{Section 4.5 of RFC9083}}

The following is an example of filterSet that might be served by an RIR.

~~~ json
{
  "objectClassName": "irr0_filterSet",
  "handle": "FLTR-FOO",
  "filter": [ "(AS64501 or FLTR-BAR) and <AS64502>" ],
  "mp-filter": [ "{2001:db8:100::/48^+}" ],
  "remarks": [
    {
      "description": [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "entities": [
    {
      "objectClassName": "entity",
      "handle": "XXXX",
      "roles": [ "registrant" ]
    }
  ],
  "links": [
    {
      "value": "https://example.net/irr0_filterSet/FLTR-FOO",
      "rel": "self",
      "href": "https://example.net/irr0_filterSet/FLTR-FOO",
      "type": "application/rdap+json"
    }
  ],
  "events": [
    {
      "eventAction": "registration",
      "eventDate": "1990-12-31T23:59:59Z"
    },
    {
      "eventAction": "last changed",
      "eventDate": "1991-12-31T23:59:59Z"
    }
  ]
}
~~~

# Autnum Route Policies

{{Section 3.1.2 of RFC9082}} defines the basic search for autnum objectClass.
The returned JSON object for Autnum search May include "irr_policies" object member.
"irr_policies" is an optional and must be an array, the order of the objects in the array is to be observed during processing.

"irr0_policies" can contain following object member and each of them is a string containing a value as specified by RPSL:

* "import" -- see {{Section 6.1 of RFC2622}}
* "mp-import" -- see {{Section 2.5 of RFC4012}}
* "import-via" -- see {{I-D.ietf-grow-rpsl-via}}
* "export" -- see {{Section 6.2 of RFC2622}}
* "mp-export" -- see {{Section 2.5 of RFC4012}}
* "export-via" -- see {{I-D.ietf-grow-rpsl-via}}

An example "irr_policies" data structure:

~~~ json
"irr0_policies": [
  { "import-via": "ASXXX from AS-ANY EXCEPT (ASXXX AND ASYYY) accept ANY" },
  { "export-via": "ASXXX to AS-ANY EXCEPT (ASXXX AND ASYYY) announce AS-YYYY" }
]
~~~

# RDAP Conformance

A server that supports the functionality specified in this document MUST include the additional string literal "irr0" in the "rdapConformance" array ({{Section 4.1 of RFC9083}}) of its responses.

# Discussions

TODO Discussions

# Privacy Considerations

The search functionality defined in this document may affect the privacy of entities in the registry (and elsewhere) in various ways: see {{RFC6973}} for a general treatment of privacy in protocol specifications, and {{Section 4 of RFC7481}} for specific discussion about privacy threats with respect to the registration data provided by RDAP.
Server operators should be aware of the tradeoffs that result from implementation of this functionality.

Many jurisdictions have laws or regulations that restrict the use of "Personal Data", per the definition in {{Section 3.2 of RFC6973}}.
Given that, server operators should ascertain whether the regulatory environment in which they operate permits implementation of the functionality defined in this document.

# Security Considerations

{{RFC7481}} describes security requirements and considerations for RDAP generally.
Additionally, guidance as to the use of TLS has changed since that document was published: see {{RFC8446}} and {{BCP195}} for further detail.

{{Section 8 of RFC9082}} includes security considerations relating to object retrieval in RDAP.
Those considerations are relevant here as well.

# IANA Considerations

TODO IANA Considerations

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
