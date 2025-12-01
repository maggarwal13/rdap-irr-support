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
area: Internet
workgroup: Internet Engineering Task Force
keyword:
  - next generation
  - unicorn
  - sparkling distributed ledger
venue:
  group: regext
  type: Working Group
  mail: regext@ietf.org
  arch: https://example.com/WG
  github: maggarwal13/rdap-irr-support
  latest: https://github.com/maggarwal13/rdap-irr-suppor/LATEST

author:
  -
    fullname: Mahesh Aggarwal
    ~~organization: RIPE NCC
    email: maggarwal@ripe.net
  -
    fullname: Jasdip Singh
    organization: ARIN
    email: jasdips@arin.net
  -
    fullname: Andy Newton
    organization: ICANN
    email: andy@hxr.us

normative:

informative:

...

--- abstract

The Registration Data Access Protocol (RDAP) is used by
Regional Internet Registries (RIRs) and Domain Name Registries (DNRs)
to provide access to their resource registration information.  The
core specifications for RDAP defines core object types, but it does
not contain objects for Internet Routing Registries (IRRs). This document is
intended to address this gap.


--- middle

# Introduction

The Registration Data Access Protocol (RDAP) [RFC7480] is used by
Regional Internet Registries (RIRs) and Domain Name Registries (DNRs)
to provide access to their resource registration information.  The
core specifications for RDAP defines core object types, but it does
not contain objects for Internet Routing Registries (IRRs). This document is
intended to address this gap.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in BCP
14 [RFC2119] [RFC8174] when, and only when, they appear in all
capitals, as shown here.

Indentation and whitespace in examples are provided only to
illustrate element relationships, and are not a required feature of
this specification.

"..." in examples is used as shorthand for elements defined outside
of this document, as well as to abbreviate elements that are too
long.

# Lookup Path Segment specification

RFC9082#section-3.1 defines the simple lookup path segments for types:
'ip','autnum','domain','nameserver','entity'.

This document aims to extend this to add following path segments:

'irr0_route': Used to identify ROUTE object and associated IP address prefix and the autonomous system (AS) that originates it,

'irr0_routeSet': Used to identify route-set object

'irr0_autnumSet': Used to identify as-set object

‘irr0_rtrSet’ : Defines the name of the rtr-set

‘irr0_peeringSet’ : Specifies the name of the peering-set

‘irr0_filterSet’ : Defines the name of the filter

# The Route Object Class

It is the RDAP representation of the RPSL route class defined in rfc2622#section-4

Syntax: irr0_route/< IP prefix of the interAS route >/< AS that originates the route >

For example, the following URL would be used to find information describing route object

https://example.com/rdap/irr0_route/192.0.2.0/24/65538

The following is an elided example of a route object showing the high level structure:

    {
    "objectClassName" : "irr0_route",
    "handle" : "XXXX",
    "route" :  "192.0.2.0",
    "origin" : "1234",
    ...
    "entities" :
        [
        ...
        ],
    "links" :
        [
        ...
        ],
    ...
    }

The route object class can contain the following members:

objectClassName -- the string "irr0_route"

handle -- a string representing the registry unique identifier of the route object

route — a string representing the address-prefix for which a route is referenced; as per rfc2622#section-4

origin – a string representing  an autonomous system number for which a route is referenced; as per rfc2622#section-4

routeVersion -- a string signifying the ip protocol version of the network: "v4" signifies an route with ipv4  network, and "v6" signifies a route with ipv6 network

remarks -- see RFC9083#Section 4.3

pingable -- an array of strings each containing a value as specified in RFC5943

holes -- an array of strings each containing a value as specified in RFC2622#section-4

memberOf -- an array of strings, each containing a value as specified in RFC2622#section-4

inject -- an array of strings, each containing a value as specified in RFC2622#section-4

components - a string containing a value as specified in RFC2622#section-4

aggregateBoundary - a string containing a value as specified in RFC2622#section-4

aggregateMtd - a string containing a value as specified in RFC2622#section-4

exportComps - a string containing a value as specified in RFC2622#section-4

entities -- an array of entity objects as defined by RFC9083#Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of the JSON object

TODO Full example

# The SET Object Class

RFC2622#section-5 defines SET objects. This section aims to represent SET classes in RDAP representation.
Support for peering-set, rtr-set and filter-set is optional and may be provided at the discretion of the implementation.

## Route Set Object Class

It is the RDAP representation of the RPSL route-set class defined in rfc2622#section-5.2

Syntax: irr0_routeSet/< name of the route set >

For example, the following URL would be used to find information describing route-set object

https://example.com/rdap/irr0_routeSet/AS12329:RS-FROMRUB

The following is an elided example of a routeSet object showing the high level structure:

    {
    "objectClassName" : "irr0_routeSet",
    "handle" : "XXX",
    "members" :
        [
        ...
        ],
    …
    "entities" :
        [
        ...
        ],
    "links" :
        [
        ...
        ],
    ...
    }

The routeSet object class can contain the following members:

objectClassName -- the string “irr0_routeSet"

handle -- a string representing the registry unique identifier of the routeSet object.

members —  an array of strings, each containing a value as specified in RFC2622#section-5.2

mp-members —  an array of strings, each containing a value as specified in RFC4012#section-4.2

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by RFC9083#Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of an routeSet that might be served by an RIR.

TODO Full example

## Autnum Set Object Class

It is the RDAP representation of the RPSL autnum-set class defined in RFC2622#section-5.1

Syntax: irr0_autanumSet/< name of the as-set >

For example, the following URL would be used to find information describing autnum-set object

https://example.com/rdap/irr0_autnumSet/AS-01121978

The following is an elided example of an autnumSet object showing the high level structure:

    {
    "objectClassName" : "irr0_autnumSet",
    "handle" : "XXX",
    "members" :
        [
        ...
        ],
    …
    "entities" :
        [
        ...
        ],
    "links" :
        [
        ...
        ],
    ...
    }

The autnumSet object class can contain the following members:

objectClassName -- the string "irr0_autnumSet"

handle -- a string representing the registry unique identifier of the autnumSet object.

members —  an array of strings, each containing a value as specified in RFC2622#section-5.1

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by RFC9083#Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of an autnumSet that might be served by an RIR.

TODO Full example

## RTR Set Object Class

It is the RDAP representation of the RPSL rtr-set class defined in RFC2622#section-5.5

Syntax: irr0_rtrSet/< name of the router-set >

For example, the following URL would be used to find information describing rtrSet object

https://example.com/rdap/irr0_rtrSet/AS28816:rtrs-arbinet-customer-rs

The following is an elided example of a rtrSet object showing the high level structure:

    {
    "objectClassName" : "irr0_rtrSet",
    "handle" : "XXX",
    "members" :
        [
        ...
        ],
    "mp-members" :
        [
        ...
        ],
    …
    "entities" :
        [
        ...
        ],
    "links" :
        [
        ...
        ],
    ...
    }

The rtrSet set  object class can contain the following members:

objectClassName -- the string "irr0_rtrSet"

handle -- a string representing the registry unique identifier of the rtrSet.

members —  an array of strings, each containing a value as specified in RFC2622#section-5.5

mp-members —  an array of strings, each containing a value as specified in RFC4012#section-4.6

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5


The following is an example of rtrSet that might be served by an RIR.

TODO Full example

## Peering Set Object Class

It is the RDAP representation of the RPSL peering-set class defined in RFC2622#section-5.6

Syntax: irr0_peeringSet/< name of the peering-set >

For example, the following URL would be used to find information describing peering-set object

https://example.com/rdap/irr0_peeringSet/AS12695:PRNG-UPSTREAMS

The following is an elided example of a peeringSet object showing the high level structure:

    {
    "objectClassName" : "irr0_peeringSet",
    "handle" : "XXX",
    "peering" :
        [
        ...
        ],
    "mp-peering" :
        [
        ...
        ],

         …
    "entities" :
        [
        ...
        ],
    "links" :
        [
        ...
        ],
    ...
    }

The peeringSet  object class can contain the following members:

objectClassName -- the string “irr0_peeringSet"

handle -- a string representing the registry unique identifier of the peeringSet

peering —  an array of strings, each containing a value as specified in RFC2622#section-5.6

mp-peering —  an array of strings, each containing a value as specified in RFC4012#section-4.4

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of peeringSet that might be served by an RIR.

TODO Full example

## Filter Set Object Class

It is the RDAP representation of the RPSL filter-set class defined in RFC2622#section-5.4

Syntax: irr0_filterSet/< name of the filter >

For example, the following URL would be used to find information describing filter object

https://example.com/rdap/irr0_filterSet/AS12528:fltr-bogons

The following is an elided example of a filterSet object showing the high level structure:

    {
        "objectClassName" : "irr0_filterSet",
        "handle" : "XXX",
        "filter" :
            [
            ...
            ],
        "mp-filter" :
            [
            ...
            ],
             …
        "entities" :
            [
            ...
            ],
        "links" :
            [
            ...
            ],
        ...
    }

The filterSet  object class can contain the following members:

objectClassName -- the string "irr0_filterSet"

handle -- a string representing the registry unique identifier of the filterSet

filter —  an array of strings each defines the set's policy filter as per RFC2622#section-5.4

mp-filter —  an array of strings, each containing a value as specified in RFC4012#Section 2.5.2

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of filterSet that might be served by an RIR.

TODO Full example

# Autnum Route Policies

RFC9082#section-3.1 defines the basic search for autnum objectClass. The returned JSON object for Autnum search May include irr_policies object member. irr_policies is an optional and must be an array, the order of the objects in the array is to be observed during processing.

"irr0_policies” can contain following object member and each of them is a string containing a value as specified by RPSL:

      import

      mp-import

      import-via

      export

      mp-export

      export-via

An example irr_policies data structure:

    "irr0_policies":
        [
            { "import-via": "ASXXX from AS-ANY EXCEPT (ASXXX AND ASYYY) accept ANY" },
            { "export-via": "ASXXX to AS-ANY EXCEPT (ASXXX AND ASYYY) announce AS-YYYY" }
        ]

The following is an example of a JSON object representing an autnum with the routing policies.

TODO Full example


# RDAP Conformance

A server that supports the functionality specified in this document MUST include additional string literals “irr0” in the rdapConformance array of its responses.

# Discussions

TODO Discussions

# Privacy Considerations

The search functionality defined in this document may affect the
privacy of entities in the registry (and elsewhere) in various ways:
see [RFC6973] for a general treatment of privacy in protocol
specifications, and [RFC7481] for specific discussion about privacy
threats with respect to the registration data provided by RDAP.
Server operators should be aware of the tradeoffs that result from
implementation of this functionality.

Many jurisdictions have laws or regulations that restrict the use of
"Personal Data", per the definition in [RFC6973].  Given that, server
operators should ascertain whether the regulatory environment in
which they operate permits implementation of the functionality
defined in this document.

# Security Considerations

[RFC7481] describes security requirements and considerations for RDAP
generally.  Additionally, guidance as to the use of TLS has changed
since that document was published: see [RFC8446] and [BCP195] for
further detail.

[RFC9082] includes security considerations relating to object
retrieval in RDAP.  Those considerations are relevant here as well.

# IANA Considerations

TODO IANA Considerations

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
