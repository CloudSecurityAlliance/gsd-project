# Comments on NIST SP 800-216

https://csrc.nist.gov/publications/detail/sp/800-216/draft

https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-216-draft.pdf

Please put the section name and line numbers when quoting text.

# General comments

The language in this draft is not clear, e.g. is SHOULD/MUST being used in accordance with RFC2119?

The draft appears to focus exclusively on traditional software products run by end users and appears to ignore cloud services and other newer technologies and delivery methods.

# Specific comments below

## U.S. Government Vulnerability Disclosure

```
235 Thousands of security vulnerabilities in computer software and systems are discovered and
236 publicly disclosed every year. Likely, even more are discovered by developers and quietly fixed
```
Thousands is on the low end, there are ~16000 CVEs assigned yearly (by CVE Identifier YEAR, for the last 4 years. For example a quick search of GitHub shows hundreds of thousands: https://github.com/search?q=%22security+fix%22 and this ignores the cloud services, and non english speaking world largely.

```
237 without anyone ever being aware. In 2020 alone, there were over 18,000 publicly listed
```

This number is unclear. By Assigned data and by YEAR in the CVE ID:

```
curl https://cve.mitre.org/data/downloads/allitems.csv | grep -a "^CVE-2020-" | grep -v "\* RESERVED \*" | wc -l
17802

curl https://cve.mitre.org/data/downloads/allitems.csv | grep -a "Assigned (2020[0-9][0-9][0-9][0-9]" | grep -v "\* RESERVED \*" | wc -l
17000
```

The git repo may have different data but walking all the files to extract the time they actually went public with data needs to be done at some point.

```
335 In the context of this document, the term “vulnerability” refers to a security vulnerability in a
336 digital product. It does not refer to other kinds of vulnerabilities that may pertain to, for example,
337 physical security, economic security, or foreign policy issues.
```

Assuming digital products includes cloud services then physical security is a valid concern. Please note that the word "cloud" only occurs once in the document in a reference to ISO IEC 27017. This creates a significant blindspot as 1) many government agencuies use cloud services and 2) many software and "digital products" make use of cloud services (licensing management, updates, data storage and processing, etc.). 

```
397 Each FCB participant should develop the ability to receive vulnerability reports from reporters,
398 maintain a database of received reports, and engage in secure communications (e.g., using a
399 report tracking system). The expectation for communication should be established, including the
400 initial acknowledgment, status updates, and agreed method of communication. The actual receipt
401 of a vulnerability report may take multiple forms (e.g., email, web forms, or a phone hotline) and
402 should be stated in a public policy
```

Where will these policies be published, and how will people find them? There are no generally accepted standards here, e.g. do they use domain.tld/security/ or domain.tld/security.txt (https://securitytxt.org/) or simply rely on al ink in the front page or the "contact us" page? Discovery of how to report an issue is problematic and can result in people giving up and not reporting issues, or extra time being required during an emergency to find out whom to contact and how to contact them.

```
408 Vulnerability reports should include a description of the product or service affected; how the
409 potential vulnerability can be identified, demonstrated, or reproduced; and what type of
410 functional impact the vulnerability allows. Due to the sensitivity of the information, agencies
411 should provide mechanisms for confidentially receiving additional information within the reports
412 (e.g., web forms, bug or issue tracking systems, vulnerability reporting services, email, or role
413 address independent of any individual). To facilitate verification of the vulnerability, agencies
414 should design the reporting mechanisms that lead to better information in assessing the validity,
415 severity, scope, and impact of vulnerabilities. This information could include:
```

No mention is made of reporting formats or standards, e.g. CVE JSON format? CSAF? OSV? UVI?

```
430 Prior to the receipt of any vulnerabilities, each FCB participant will determine which government
431 VDPOs fall within the scope of their services. The FCB entity will then obtain and maintain a list
432 of VDPO contacts within the relevant government agencies that receive and handle vulnerability
```

This appears to assume a traditional top down pyramid structure, is there any thought giving to lateral reporting or more of a matrix style layout to allow multiple pathways? Top-down reporting strucutres tend to suffer from the fact they are entirely comprised of a chain of single paths of failure.

```
521 Public disclosure may be considered if:
522 • The specific vulnerability is not publicly known (i.e., does not have a CVE number);
```

It is not clear if this advice implies that a CVE identifier should be obtained or not. 

```
531 In many cases, public disclosure might not be necessary or even recommended. For example,
532 publication is likely unnecessary if the vulnerable system is a service that government staff have
533 fixed and they can verify that the vulnerability was not exploited. Vulnerabilities that have been
534 fixed and had no impact on the system userbase should likely not be publicly disclosed in order
535 to enable the advisory systems to focus on vulnerabilities that require user action for continued
536 security and privacy.
```

This may create an incentive to cover security vulnerabilities up with a "we fixed it and we're pretty sure nobody exploited it" creating a false sense of security for end users. I would suggest it is better to report incidents, even onces that have been fully handled and pose no significant risk, and 1) label them as such "no action required" and 2) it allows for the creation of actual data and statistics, e.g. a system has 100 security vulnerabilities that were closed out before they became a problem, is this an indication of a security team that is really on the ball, or a team that is covering up real vulnerabilities as "not a problem" and so on? Without any data and reporting there is a strong possibility for institutional rot to set in.

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
