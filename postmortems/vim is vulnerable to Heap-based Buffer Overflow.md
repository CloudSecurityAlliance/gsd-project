# "vim is vulnerable to Heap-based Buffer Overflow" 

https://nvd.nist.gov/vuln/search/results?form_type=Basic&results_type=overview&query=vim+is+vulnerable+to+Heap-based+Buffer+Overflow&search_type=all&isCpeNameSearch=false

These CVE's all have the exact same description:

CVE-2021-3927
CVE-2021-3903
CVE-2021-3872
CVE-2021-3875
CVE-2021-3778
CVE-2021-3770

It appears someone fuzzed vim and then released the results piecemeal resul;ting in multiple CVEs rather than a single CVE for multiple issues within the same version/vulnerability type, etc. 

TODO: confirm same reporter, timelines

TODO: The CVSS scores are all different, this needs investigation.
