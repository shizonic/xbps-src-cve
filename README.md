### xbps-src-cve

This is a bash script that integrates with Void Linux's xbps-src.

#### Operation

1. Download the nvd cve database from 2002 to 2018 and modified and
processes them using 'xstlproc' with [cvechecker's](https://github.com/sjvermeu/cvechecker) nvdcve2simple.xsl.

2. find the xbps-src sourcedir and sources the template to get pkgname=
and version=

3. check if cve-check is also in the same directory as the template and
source it as well

4. use awk to get CVE entries that match the package and version from the
processed csv files

5. if entries are found separate them into cve and sev variables and check
the following:

- There is a patch named after the CVE, if found assume the CVE is fixed
- Check the patches for the CVE string and if found assume the CVE is fixed
- check if the CVE is available in the ignores= variable

6. Print out 'CVE: $CVE SEVERTITY: $SEVERITY'

#### LICENSE

cve-check is licensed under BSD-2-Clause, the same as xbps-src

nvdcve2simple.xsl is part of cvechecker which is under GPL-3.0-or-later

