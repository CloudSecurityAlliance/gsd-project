# Comments on NIST SP 800-216

https://csrc.nist.gov/publications/detail/sp/800-216/draft

https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-216-draft.pdf

Please put the section name and line numbers when quoting text.

## U.S. Government Vulnerability Disclosure

```
235 Thousands of security vulnerabilities in computer software and systems are discovered and
236 publicly disclosed every year. Likely, even more are discovered by developers and quietly fixed
```
Thousands is on the low end, there are ~16000 CVEs assigned yearly (by CVE Identifier YEAR, for the last 
4 years. For example a quick search of GitHub shows hundreds of thousands: https://github.com/search?q=%22security+fix%22

```
237 without anyone ever being aware. In 2020 alone, there were over 18,000 publicly listed
```

This number is unclear. By Assigned data and by YEAR in the CVE ID:

```
curl https://cve.mitre.org/data/downloads/allitems.csv | grep -a "^CVE-2020-" | grep -v "\* RESERVED \*" | wc -l
17248

curl https://cve.mitre.org/data/downloads/allitems.csv | grep -a "Assigned (2020[0-9][0-9][0-9][0-9]" | grep -v "\* RESERVED \*" | wc -l
15984
```

The git repo may have different data but walking all the files to extract the time they actually went public with data needs to be done at some point.

```
628 The National Vulnerability Database [NVD] is the U.S. Government repository of standards-
629 based vulnerability management data. It contains a database of almost all publicly disclosed
630 vulnerabilities — more specifically, all vulnerabilities included within the Common
631 Vulnerabilities and Exposures (CVE) dictionary [CVE]. NVD staff analyzes vulnerability
```

The CVE database is missing a huge amount of content:

1) CVEs that have been assigned, but the data not pushed back to the database (some of which is over 10 years old): https://github.com/distributedweaknessfiling/distributedweaknessfiling.org/tree/main/reserved-but-public
2) Many CNAs have security vulnerabilities and advisories with no CVE IDs, e.g. XEN (goto https://xenbits.xen.org/xsa/ and look for "none (yet) assigned")
3) Non CNA data sources with in scope content
4) Non CNA sources with "out of scope" but useful data (e.g. services, malware, backdoors, etc.)

```
794 3.2.2. Monitoring of Vulnerability Reports
795 VDPOs should monitor their reporting mechanisms for new reports and communications related
796 to existing reports. VDPOs should also monitor public sources for vulnerability reports and
797 organizational communications channels that are likely to receive vulnerability reports, such as
798 customer service and support.
```

The CVE database doesn't support this well, witness the 20,000+ missing SUSE URLs: https://github.com/distributedweaknessfiling/securitylist/commit/b690b4b1de7afba26c849e12b4aaadafc95e7e81 and 20,000+ missing Red Hat URLs: https://github.com/distributedweaknessfiling/securitylist/commit/e0a8925c90b1b4e6203fecbc6f61dcefe1b4accc
