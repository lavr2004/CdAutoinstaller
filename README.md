# CdAutoinstaller

Is an application to that get every URL to setup and make an output *.cdp project as a result

## Vocabulary
- **sourceurlStr** - input external URL string that need to be installed on CD parser after dedublication and indexing
- **sourceurlindexStr** - artefact constructed from **sourceurlStr** using special patterns table

## Main functionality modules
- **module01_DoublicatesIdentifier** - provides indexation of **sourceurlStr** and identification if it new URL for current pool of installed URLs or this URL already installed
- **module02_InstallerByTemplate** - provides installation every **sourceurlStr** using x.cdp template if module01_DoublicatesIdentifier identified target **sourceurlStr** as a new one
---
## Workflow of every module
 
### Workflow of main functionality module: **module01_DoublicatesIdentifier**
- getting **sourceurlStr** from external actor
- indexing **sourceurlStr** using table of patterns creating **sourceurlindexStr**
- loading into memory list of already installed indexed urls from staff
- search **sourceurlindexStr** of current **sourceurlStr** between same indexes of already installed URLs
- if found: mark current **sourceurlStr** as a doublicate and already installed URL. Save reference to original URL already installed for reporting
- if not found: mark current **sourceurlStr** as a new one URL never installed
- return: boolean result of result and reference to original URL already installed

![alt text](https://gc.onliner.by/images/logo/onliner_logo.v3.png)

### Workflow of main functionality module: **module02_InstallerByTemplate**
- get **sourceurlStr** need to be installed from external Actor
- checking presented **sourceurlStr** by list of patterns to get identify what parser template can be used for installation
  - if found pattern inside URL: ***make installation of current URL into one of templates referenced to pattern***
  - if not found pattern inside URL: go to identification template by page content
    - make request URL from HOST using headless browser
    - execute JavaScript to collect all < iframes > from page together
    - searching specific text pattern on the page content
    - if found pattern: ***make installation of current URL into one of templates referenced to pattern***
    - if not found pattern: make installation of current URL into general .cdp template
- return: boolean result of operations runtime


<!---markdown completed using https://dillinger.io/ web application -->
