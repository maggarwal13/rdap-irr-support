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
this protocol.

"..." in examples is used as shorthand for elements defined outside
of this document, as well as to abbreviate elements that are too
long.

# Lookup Path Segment specification

RFC9082#section-3.1 defines the simple lookup path segments for types:
'ip','autnum','domain','nameserver','entity'.

This document aims to extend this to add following path segments:

'route': Used to identify ROUTE object and associated IP address prefix and the autonomous system (AS) that originates it,

'routeSet': Used to identify route-set object

'autnumSet': Used to identify as-set object

‘rtrSet’ : Defines the name of the rtr-set

‘peeringSet’ : Specifies the name of the peering-set

‘filterSet’ : Defines the name of the filter

# The Route Object Class

It is the RDAP representation of the RPSL route class.

Syntax: route/< IP prefix of the interAS route >< AS that originates the route >

For example, the following URL would be used to find information describing route object

https://example.com/rdap/route/2a05:dfc6:9300::/40AS46138

The following is an elided example of a route object showing the high level structure:

    {
    "objectClassName" : "route",
    "handle" : "XXX",
    "prefix" : { .... },
    "origin" : { .... },
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

objectClassName -- the string “route"

handle -- a string representing the unique identifier of the route which is a combination of IP network  and an autonomous system number for which route is registered

origin – represents  an autonomous system number Object for which a route is referenced; see Section RFC9083#5.5

prefix — represents the IP network Object for which a route is referenced; see RFC9083#Section 5.4

routeVersion -- a string signifying the ip protocol version of the network: "v4" signifies an route with ipv4  network, and "v6" signifies a route with ipv6 network

remarks -- see RFC9083#Section 4.3

country -- a string containing the two-character country code of the route

pingable -- an array of IP network objects as defined in RFC9083#Section 5.4

holes -- an array of IP network objects as defined in RFC9083#Section 5.4

memberOf -- an array of SET objects as defined in the below section.

inject -- an array of strings, each containing a value as specified  by RPSL.

components - a string containing a value as specified by RPSL.

aggregateBoundary - a string containing a value as specified by  RPSL.

aggregateMtd - a string containing a value as specified by RPSL.

exportComps - a string containing a value as specified by RPSL.

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of the JSON object

TODO Full example

#   The SET Object Class

rfc2622#section-5.1 defines SET objects and these can be as-set, route-set, rtr-set,
filter-set and peering-set classes. This section aims to represent SET classes in RDAP representation.


##    Route Set Object Class

‘routeSet’ The routeSet object class is an RDAP representation of the route-set object in RPSL.

Syntax: routeSet/< name of the route set >

For example, the following URL would be used to find information describing route-set object

https://example.com/rdap/routeSet/AS12329:RS-FROMRUB

The following is an elided example of a routeSet object showing the high level structure:

    {
    "objectClassName" : "routeSet",
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

The "handle" member is the unique identifier of the routeSet object.
The "members" is an array of strings which could be a list of address-prefixes or route-set-names as per rfc2280#section-5.1

The route set  object class can contain the following members:

objectClassName -- the string “routeSet"

handle -- a string representing the unique identifier of the routeSet.

members —  an array of strings

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of an routeSet that might be served by an RIR.

TODO Full example

##    Autnum Set Object Class

‘autnumSet’ The autnumSet object class is an RDAP representation of the as-set object in RPSL as per RFC2622#5.1.

Syntax: autanumSet/< name of the as-set >

For example, the following URL would be used to find information describing autnum-set object

https://example.com/rdap/autnumSet/AS-01121978

The following is an elided example of an autnumSet object showing the high level structure:

    {
    "objectClassName" : "autnumSet",
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

The "handle" member is the unique identifier of the route-set object.
The "members" is an array of strings which could be a list of as-numbers or as-set-names as per rfc2280#section-5.2

The autnumSet  object class can contain the following members:

objectClassName -- the string “autnumSet"

handle -- a string representing the unique identifier of the autnumSet.

members —  an array of strings

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of an autnumSet that might be served by an RIR.

TODO Full example

##    RTR  Set Object Class

‘rtrSet’ The rtrSet object class is an RDAP representation of the rtr-set object in RPSL.

Syntax: rtrSet/< name of the router-set >

For example, the following URL would be used to find information describing rtrSet object

https://example.com/rdap/rtrSet/AS28816:rtrs-arbinet-customer-rs

The following is an elided example of a rtrSet object showing the high level structure:

    {
    "objectClassName" : "rtrSet",
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

objectClassName -- the string “rtrSet"

handle -- a string representing the unique identifier of the rtrSet.

members —  an array of strings

mp-members —  an array of strings

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5


The following is an example of rtrSet that might be served by an RIR.

TODO Full example

##    Peering  Set Object Class

‘peeringSet’ The peeringSet object class is an RDAP representation of the peering-set object in RPSL.

Syntax: peeringSet/< name of the peering-set >

For example, the following URL would be used to find information describing peering-set object

https://example.com/rdap/peeringSet/AS12695:PRNG-UPSTREAMS

The following is an elided example of a peeringSet object showing the high level structure:

    {
    "objectClassName" : "peeringSet",
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

objectClassName -- the string “peeringSet"

handle -- a string representing the unique identifier of the peeringSet

peering —  an array of strings each defines a peering that can be used for importing or exporting routes

mp-peering —  an array of strings each defines a multiprotocol peering that can be used for importing or exporting routes

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of peeringSet that might be served by an RIR.

TODO Full example

##    Filter Set Object Class

‘filterSet’ The filterSet object class is an RDAP representation of the filter-set object in RPSL.

Syntax: filterSet/< name of the filter >

For example, the following URL would be used to find information describing filter object

https://example.com/rdap/filterSet/AS12528:fltr-bogons

The following is an elided example of a filterSet object showing the high level structure:

    {
        "objectClassName" : "filterSet",
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

objectClassName -- the string “filterSet"

handle -- a string representing the unique identifier of the filterSet

filter —  an array of strings each defines the set's policy filter

mp-filter —  an array of strings each defines the set's multiprotocol policy filter

remarks -- see RFC9083#Section 4.3

entities -- an array of entity objects as defined by Section 5.1

links -- see RFC9083#Section 4.2

port43 -- see RFC9083#Section 4.7

events -- see RFC9083#Section 4.5

The following is an example of filterSet that might be served by an RIR.

TODO Full example

# Autnum Route Policies

RFC9082#section-3.1 defines the basic search for autnum objectClass. The returned JSON object for Autnum search May include irr_policies object member. irr_policies is an optional and must be an array, the order of the objects in the array is to be observed during processing.

“irr_policies” can contain following object member and each of them is a string containing a value as specified by RPSL:

      import

      mp-import

      import-via

      export

      mp-export

      export-via

An example irr_policies data structure:

    "irr_policies":
        [
            { "import-via": "ASXXX from AS-ANY EXCEPT (ASXXX AND ASYYY) accept ANY" },
            { "export-via": "ASXXX to AS-ANY EXCEPT (ASXXX AND ASYYY) announce AS-YYYY" }
        ]

The following is an example of a JSON object representing an autnum with the routing policies.

TODO Full example


# RDAP Conformance

A server that supports the functionality specified in this document MUST include additional string literals “irrRdap1” in the rdapConformance array of its responses.

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
