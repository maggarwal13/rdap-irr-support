# Introduction

In order to decide which IRR object types and attributes to support in the RDAP IRR specification, we need to examine
the IRR databases in each RIR to see what is currently supported.

An RIR objects analysis was performed for the RIR Internet Numbers Registries (INR)
in [RFC 7485: Inventory and Analysis of WHOIS Registration Objects](https://www.rfc-editor.org/info/rfc7485/).

For this analysis we
use [RFC 2622: Routing Policy Specification Language (RPSL)](https://www.rfc-editor.org/info/rfc2622/) as a starting
point.

# Open Questions

* What are the similarities in IRR object types between RIRs? Can we reduce this to a common minimum set that we need to
  support?
* Are there any RIR-specific differences that are not common but that we should also support?
* Are there any object types or attributes which are not much used and do not need to be supported (e.g. inet-rtr) ?
* Are there any differences in third-party IRR databases which should also be supported?

# AUT-NUM

| RIPE           | ARIN          | APNIC          | AFRINIC    | LACNIC      |
|----------------|---------------|----------------|------------|-------------|
| aut-num        | aut-num       | aut-num        | aut-num    | aut-num     |
| as-name        | as-name       | as-name        | as-name    | N/A         |
| descr          | descr         | descr          | descr      | N/A         |
| member-of      | member-of     | member-of      | member-of  | N/A         |
| import-via     | N/A           | import-via     | N/A        | N/A         |
| import         | import        | import         | import     | N/A         |
| mp-import      | mp-import     | mp-import      | mp-import  | N/A         |
| export-via     | N/A           | export-via     | N/A        | N/A         |
| export         | export        | export         | export     | N/A         |
| mp-export      | mp-export     | mp-export      | mp-export  | N/A         |
| default        | default       | default        | default    | N/A         |
| mp-default     | mp-default    | mp-default     | mp-default | N/A         |
| remarks        | N/A           | remarks        | remarks    | N/A         |
| org            | N/A           | org            | org        | N/A         |
| sponsoring-org | N/A           | sponsoring-org | N/A        | N/A         |
| admin-c        | admin-c       | admin-c        | admin-c    | N/A         |
| tech-c         | tech-c        | tech-c         | tech-c     | N/A         |
| abuse-c        | N/A           | abuse-c        | N/A        | N/A         |
| status         | N/A           | N/A            | status     | N/A         |
| notify         | N/A           | notify         | notify     | N/A         |
| mnt-by         | mnt-by        | mnt-by         | mnt-by     | N/A         |
| created        | N/A           | N/A            | N/A        | N/A         |
| last-modified  | last-modified | last-modified  | N/A        | N/A         |
| N/A            | N/A           | N/A            | N/A        | owner       |
| N/A            | N/A           | N/A            | N/A        | ownerid     |
| N/A            | N/A           | N/A            | N/A        | responsible |
| N/A            | N/A           | N/A            | N/A        | address     |
| N/A            | N/A           | N/A            | N/A        | country     |
| N/A            | N/A           | N/A            | N/A        | phone       |
| N/A            | N/A           | N/A            | N/A        | owner-c     |
| N/A            | N/A           | N/A            | N/A        | routing-c   |
| N/A            | N/A           | N/A            | N/A        | abuse-c     |
| N/A            | N/A           | N/A            | N/A        | inetnum     |
| N/A            | N/A           | country        | N/A        | N/A         |
| N/A            | N/A           | mnt-lower      | mnt-lower  | N/A         |
| N/A            | N/A           | mnt-routes     | mnt-routes | N/A         |
| N/A            | N/A           | N/A            | changed    | N/A         |
| N/A            | N/A           | N/A            | mnt-irt    | N/A         |

# AS-SET

| RIPE          | ARIN           | APNIC         | AFRINIC     | LACNIC  |
|---------------|----------------|---------------|-------------|---------|
| as-set        | as-set         | as-set        | as-set      | as-set  |
| descr         | descr          | descr         | descr       | descr   |
| members       | members        | members       | members     | members |
| mbrs-by-ref   | members-by-ref | mbrs-by-ref   | mbrs-by-ref | N/A     |
| remarks       | remarks        | remarks       | remarks     | N/A     |
| org           | N/A            | org           | org         | N/A     |
| tech-c        | tech-c         | tech-c        | tech-c      | N/A     |
| admin-c       | admin-c        | admin-c       | admin-c     | N/A     |
| notify        | N/A            | notify        | notify      | N/A     |
| mnt-by        | mnt-by         | mnt-by        | mnt-by      | mnt-by  |
| mnt-lower     | N/A            | mnt-lower     | mnt-lower   | N/A     |
| created       | created        | N/A           | N/A         | N/A     |
| last-modified | last-modified  | last-modified | N/A         | N/A     |
| N/A           | changed        | N/A           | changed     | changed |
| N/A           | N/A            | country       | N/A         | N/A     |

# FILTER-SET

| RIPE          | ARIN | APNIC         | AFRINIC    | LACNIC |
|---------------|------|---------------|------------|--------|
| filter-set    | N/A  | filter-set    | filter-set | N/A    |
| descr         | N/A  | descr         | descr      | N/A    |
| filter        | N/A  | filter        | filter     | N/A    |
| mp-filter     | N/A  | mp-filter     | mp-filter  | N/A    |
| remarks       | N/A  | remarks       | remarks    | N/A    |
| org           | N/A  | org           | org        | N/A    |
| tech-c        | N/A  | tech-c        | tech-c     | N/A    |
| admin-c       | N/A  | admin-c       | admin-c    | N/A    |
| notify        | N/A  | notify        | notify     | N/A    |
| mnt-by        | N/A  | mnt-by        | mnt-by     | N/A    |
| mnt-lower     | N/A  | mnt-lower     | mnt-lower  | N/A    |
| created       | N/A  | N/A           | N/A        | N/A    |
| last-modified | N/A  | last-modified | N/A        | N/A    |
| N/A           | N/A  | N/A           | changed    | N/A    |

# INET-RTR

Out of scope?

# PEERING-SET

| RIPE          | ARIN | APNIC         | AFRINIC     | LACNIC |
|---------------|------|---------------|-------------|--------|
| peering-set   | N/A  | peering-set   | peering-set | N/A    |
| descr         | N/A  | descr         | descr       | N/A    |
| peering       | N/A  | peering       | peering     | N/A    |
| mp-peering    | N/A  | mp-peering    | mp-peering  | N/A    |
| remarks       | N/A  | remarks       | remarks     | N/A    |
| org           | N/A  | org           | org         | N/A    |
| tech-c        | N/A  | tech-c        | tech-c      | N/A    |
| admin-c       | N/A  | admin-c       | admin-c     | N/A    |
| notify        | N/A  | notify        | notify      | N/A    |
| mnt-by        | N/A  | mnt-by        | mnt-by      | N/A    |
| mnt-lower     | N/A  | mnt-lower     | mnt-lower   | N/A    |
| created       | N/A  | N/A           | N/A         | N/A    |
| last-modified | N/A  | last-modified | N/A         | N/A    |
| N/A           | N/A  | N/A           | changed     | N/A    |

# ROUTE(6)

| RIPE          | ARIN      | APNIC         | AFRINIC      | LACNIC   |
|---------------|-----------|---------------|--------------|----------|
| route(6)      | route     | route(6)      | route(6)     | route(6) |
| descr         | descr     | descr         | descr        | descr    |
| origin        | origin    | origin        | origin       | origin   |
| pingable      | N/A       | N/A           | N/A          | N/A      |
| ping-hdl      | N/A       | N/A           | N/A          | N/A      |
| holes         | N/A       | holes         | holes        | N/A      |
| org           | N/A       | org           | org          | N/A      |
| member-of     | member-of | member-of     | member-of    | N/A      |
| inject        | N/A       | inject        | inject       | N/A      |
| aggr-mtd      | N/A       | aggr-mtd      | aggr-mtd     | N/A      |
| aggr-bndry    | N/A       | aggr-bndry    | aggr-bndry   | N/A      |
| export-comps  | N/A       | export-comps  | export-comps | N/A      |
| components    | N/A       | components    | components   | N/A      |
| remarks       | remarks   | remarks       | remarks      | remarks  |
| notify        | N/A       | notify        | notify       | N/A      |
| mnt-lower     | N/A       | mnt-lower     | mnt-lower    | N/A      |
| mnt-routes    | N/A       | mnt-routes    | mnt-routes   | N/A      |
| mnt-by        | mnt-by    | mnt-by        | mnt-by       | mnt-by   |
| created       | N/A       | N/A           | N/A          | N/A      |
| last-modified | N/A       | last-modified | N/A          | N/A      |
| N/A           | admin-c   | N/A           | N/A          | N/A      |
| N/A           | tech-c    | N/A           | N/A          | N/A      |
| N/A           | N/A       | country       | N/A          | N/A      |
| N/A           | N/A       | N/A           | changed      | changed  |

# ROUTE-SET

| RIPE          | ARIN          | APNIC         | AFRINIC     | LACNIC |
|---------------|---------------|---------------|-------------|--------|
| route-set     | route-set     | route-set     | route-set   | N/A    |
| descr         | descr         | descr         | descr       | N/A    |
| members       | members       | members       | members     | N/A    |
| mp-members    | mp-members    | mp-members    | mp-members  | N/A    |
| mbrs-by-ref   | mbrs-by-ref   | mbrs-by-ref   | mbrs-by-ref | N/A    |
| remarks       | remarks       | remarks       | remarks     | N/A    |
| org           | N/A           | org           | org         | N/A    |
| tech-c        | tech-c        | tech-c        | tech-c      | N/A    |
| admin-c       | admin-c       | admin-c       | admin-c     | N/A    |
| notify        | N/A           | notify        | notify      | N/A    |
| mnt-by        | mnt-by        | mnt-by        | mnt-by      | N/A    |
| mnt-lower     | N/A           | mnt-lower     | mnt-lower   | N/A    |
| created       | created       | N/A           | N/A         | N/A    |
| last-modified | last-modified | last-modified | N/A         | N/A    |
| N/A           | changed       | N/A           | changed     | N/A    |

# RTR-SET

| RIPE          | ARIN | APNIC         | AFRINIC     | LACNIC |
|---------------|------|---------------|-------------|--------|
| rtr-set       | N/A  | rtr-set       | rtr-set     | N/A    |
| descr         | N/A  | descr         | descr       | N/A    |
| members       | N/A  | members       | members     | N/A    |
| mp-members    | N/A  | mp-members    | mp-members  | N/A    |
| mbrs-by-ref   | N/A  | mbrs-by-ref   | mbrs-by-ref | N/A    |
| remarks       | N/A  | remarks       | remarks     | N/A    |
| org           | N/A  | org           | org         | N/A    |
| tech-c        | N/A  | tech-c        | tech-c      | N/A    |
| admin-c       | N/A  | admin-c       | admin-c     | N/A    |
| notify        | N/A  | notify        | notify      | N/A    |
| mnt-by        | N/A  | mnt-by        | mnt-by      | N/A    |
| mnt-lower     | N/A  | mnt-lower     | mnt-lower   | N/A    |
| created       | N/A  | N/A           | N/A         | N/A    |
| last-modified | N/A  | last-modified | N/A         | N/A    |
| N/A           | N/A  | N/A           | changed     | N/A    |










