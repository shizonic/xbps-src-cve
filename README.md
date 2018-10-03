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

6. Store the cve and severity and print out the format:

PKG (PKGNAME) VERSION:
  CVE-NUM CVE-SEV
  [...]

PKG -> Name of the package on the template
PKGNAME -> Name of the package after sourcing cve-check and doing changes to
VERSION -> Version of the package after sourcing cve-check
CVE-NUM -> CVE number with CVE- prefix
CVE-SEV -> CVE severity

#### FAQ

Q: Why integrate it with xbps-src

A: Like update-check, xbps-src is arch-independent and we can make use of our
equivalent to the update file (cve-check) for some flexiblity, like ignoring
CVEs that don't apply and fixing the version= and pkgname= variables if we 
don't follow the ones in upstrea.

Q: Why bash, awk, libxslt and wget

A: I wanted the least dependencies as possible when dealing with this and i'm
decent with bash which is already required for using xbps-src

if pushed for maximum speed 'xsv' (which is written in rust) would be used

Q: Is it official ?

A: Not at the moment and most likely this will have a completely different face
if it becomes


#### TODO

- Find a way to get rid of nvdcve2simple.xsl (Permissive alternative?)
- Make it proper for merging into xbps-src

- Optimize (ideas)
	- Make a single awk call for all packages
	- Remove lots of garbage from the csv files when they are first processed (OSes and Hardware)

#### LICENSE

cve-check is licensed under BSD-2-Clause, the same as xbps-src

nvdcve2simple.xsl is part of cvechecker which is under GPL-3.0-or-later

