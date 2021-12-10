# Thoughts on data formats

This is not a final document nor an official statement on the data format(s) used by the GSD. This is designed to help structure and encourage discussion around vulnerbaility identifer data formats.

The GSD can use other peoples data formats, especially if we clearly label them as such. We can also provide mappings, e.g. OSV:affected:package:name maps to CVE:product:product_name to translate the data and make it easier to consume.

## a GSD Identifier MUST have:

* Identifier
* Meta data (time assigned, who requested it, etc.)
* Reference URL (optional: type of URL, copy of data, etc.) OR Source (e.g. a namespace and an identifier, "redhat.com:RHSA-2021-1234" OR known exploit OR known exploitation

Essentially we need some path if discoverability. 

## a GSD Identifier SHOULD have

* Affected / Fixed / Vulnerable / Not Vulnerable products/services (CPE? JSON? Purl?)
* Vulnerbaility information/type (e.g. CWE)

And ideally we want some information to make the security identifier directly useful for systems and humans beings that consume the data.

## a GSD Identifier CAN have:

* Text description
* Severity scores
* Relationship data (parent/child/sibling/etc of)
* Exploits (code/reproducers)
* Exploitation (knowledge of exploitation)
* Patches
* Workarounds
* Configuration related information


## Other data format examples:

* CPE https://nvd.nist.gov/products/cpe
* CSAF2 https://docs.oasis-open.org/csaf/csaf/v2.0/csd01/csaf-v2.0-csd01.html
* CVE https://github.com/CVEProject/cve-schema/tree/master/schema
* CWE https://cwe.mitre.org/community/submissions/guidelines.html
* CVRF https://www.icasi.org/cvrf/
* OSV https://ossf.github.io/osv-schema/
* OVAL https://oval.mitre.org/

## String and value handling

Anything that is a string or a value that can be more than one value needs to be a list so that multiple values can be clearly supported. A perfect example of this is (GSD-2021-1002352.json)[https://github.com/cloudsecurityalliance/gsd-database/blob/main/2021/1002xxx/GSD-2021-1002352.json] which is called "log4j" and "log4j2" by Apache and other organizations use the names interchangeably it appears. This means that anything that is not clearly defined as having only a single possible value (e.g. the GSD ID itself, the assigned time) must be assumed to potentially be a list of values.
