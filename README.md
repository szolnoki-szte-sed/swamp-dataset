# CVEPoisonKnowledgebase

The collection of poisoned code snippets that are officially identified with a CVE identifier.

## Content of this repository
* Vulnerable code snippets
* Metadata for the vulnerable code snippets

### Vulnerable code snippets
We have them in separate folders, organized by source and programming language. For example, at `CWE-mitre\C`, you can find the vulnerable code snippets in C language from the source `CWE-mitre`. An example of such code is where we only have a single line that has been removed:
```
-pwd = getpwnam(getlogin());if (isTrustedGroup(pwd->pw_gid)) {allow();} else {deny();}
```
### Metadata
We have a metadata file for each vulnerable code snippets, for the code snippet above this is the metadata:
```
{
    "original_source": {
        "database(url)": "https://cwe.mitre.org/",
        "software_system(CPE)": [
            "cpe:2.3:a:sendmail:sendmail:8.10:*:*:*:*:*:*:*",
            "cpe:2.3:a:beasts:vsftpd:1.2.0:*:*:*:*:*:*:*"
        ],
        "fix_commit": "",
        "version_end_excluding": {
            "sendmail:sendmail": "unknown",
            "beasts:vsftpd": "unknown"
        },
        "path": {
            "file_path": ""
        }
    },
    "programming_language": "C",
    "licences": {
        "database": "MIT",
        "affected_repository": "Unknown"
    },
    "related_vulnerability_entry": {
        "CVE": [
            "CVE-2001-1349",
            "CVE-2004-2259"
        ],
        "CWE": [
            "CWE-663"
        ]
    }
}
```
- `database(url)` indicates the source of the vulnerable code snippet.
- `software_system(CPE)` lists the affected software and its versions.
- `fix_commit` is where the known fix, if any, is listed.
- `programming_language` indicates the language of the code snippet.
- `related_vulnerability_entry` provides the related `CVE` and `CWE` identifiers.


## How the data has been collected

### CVEFixes
CVEfixes is a comprehensive vulnerability dataset that is automatically collected and curated from Common Vulnerabilities and Exposures (CVE) records in the public [U.S. National Vulnerability Database (NVD)](https://nvd.nist.gov/). It provides an SQLite file containing records about vulnerable code snippets, along with their CVE and CWE identifiers. We wrote a script to collect the vulnerable snippets into files and create metadata by using the [NVD API](https://nvd.nist.gov/developers/vulnerabilities) and the [GitHub API](https://docs.github.com/en/rest) to retrieve the license information of the projects where the vulnerabilities occurred.

### CWE-mitre
CWE MITRE is the organization responsible for curating and maintaining the CWE list. They are well-known for their work in cybersecurity, including managing other key frameworks such as CVE (Common Vulnerabilities and Exposures) and ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge). From the MITRE page, you can [download](https://cwe.mitre.org/data/downloads.html) the complete data as an XML file. We used a Python script to collect the vulnerable code snippets and, based on their CVE identifiers, gathered the commit data associated with the vulnerabilities using the [NVD API](https://nvd.nist.gov/developers/vulnerabilities). Additional information was gathered using the [GitHub API](https://docs.github.com/en/rest).

### project-KB
Project-KB provides a Java code snippet collection along with a database in CSV format. In this CSV file, we found commit information and CVE identifiers. Using this information, we collected the commits containing the vulnerable code snippets, and by using the [NVD API](https://nvd.nist.gov/developers/vulnerabilities) and [GitHub API](https://docs.github.com/en/rest), we gathered the additional information needed to build the knowledgebase.