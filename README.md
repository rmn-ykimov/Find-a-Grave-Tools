# Find a Grave Tools
Create a local stash of "Find a Grave" (https://www.findagrave.com) memorial pages.
Extract/report data.
## Last updated
2025-10-15

## Background
These python scripts were created to help Cindy Foster @ iHuntDeadPeople.com with [one of her genealogy research projects](https://ihuntdeadpeople.com/let-us-help-with-your-genealogy-research/).

Cindy is creating a book about the five protestant cemeteries in Sherrill, Iowa. The book catalogs all of the burials in those cemeteries (as well as connected family burials). Additionally, her book presents a collection of data and stories around the lives of those people.

You can read more about Cindy and her work at https://ihuntdeadpeople.com/about/

## Description
Unfortunately 'Find a Grave' does not expose a public [API](https://en.wikipedia.org/wiki/API) to programatically extract information. If we want to mine data from the website for a genealogy project, we have to [scrape](https://en.wikipedia.org/wiki/Web_scraping) pages.

Rather than continously hit live website pages for data, pages needed for a project are pulled once and stashed locally. The analysis script(s) use these stashed pages.

stash_graves.py is used to:
- PULL specific pages for specifc groups in a collection of cemeteries.
        - Leverages the [requests](https://pypi.org/project/requests/) Python package
	- An instruction file contains the cemeteries and groups to pull.
	- Cemeteries are identified by the same numeric ID 'Find a Grave' uses. 
	- Groups are: burial, parent, spouse, child, sibling, half-sibling
- STASH the pulled pages in a local directory (much like how a cache works).

dig_graves.py is used to:
- EXTRACT the data
	- Leverages the [Beautiful Soup](https://pypi.org/project/beautifulsoup4/) Python package
- REPORT data to a saved Excel spreadsheet
	- Uses the [XlsxWriter](https://pypi.org/project/XlsxWriter/) Python package

## Operation
1. Edit 'instructions/stash_graves.txt' to include the cemeteries and groups to pull from 'Find a Grave'.
   - Do not forget to read and follow the 'Schema' rules section. This includes creating a unique abbreviation for each
     cemetery (e.g. PRES, UMC, ...) and appending it after the cemetery id (e.g. 2353265-PRES, 2136908-UMC, ...). It will
     be used as the tab name on the final spreadsheet created by 'dig-graves.py.'
   - The default operation is to create a log file for each cemetery. It is located in the /logs folder. Tn not create a
     log, preceed the the word "log" (which is on a line by itself) with the # comment symbol. 
2. Run 'python stash_graves.py' to create a local stash of the pages.
   - Stashes are named by cemetery and located in the /stash folder. If you move or rename them, 'dig-graves.py' will fail.
3. Edit 'instructions/dig_graves.txt' to include which cemeteries to pull from the stashed pages.
4. Run 'python dig_graves.py'.
5. The output spreadsheet will be in '/output/burials.xlsx'.

## Python Notes
1.  These scripts were run on Mac OS 26.0.1, inside a venv (Python virtual environment), using Python version 3.14.0 [2025-10-15].
2.  Make sure you have Python installed. Mine is in /usr/bin and was installed using the Homebrew (https://brew.sh) package manager.
3.  Make a project directory on your computer. Download all the files from this repo into the directory.
4.  Create a .venv directory in your project directory using "python3 -m venv .venv"
5.  From the project directory, activate the venv using "source .venv/bin/activate" (use "deactivate" to leave the venv)
6.  Your command line prompt will change now be preceeded with a (.venv): e.g. doug% will become (.venv) doug%
7.  When the venv is created, the "pip3" command will be installed in .venv/bin/pip3
8.  Install the packages: "pip3 install requests", "pip3 install beautifulsoup4", "pip3 install xlsxwriter"
9.  List all packages in your venv using "pip3 list"
    Package            Version
    ------------------ ---------
    beautifulsoup4     4.14.2
    certifi            2025.10.5
    charset-normalizer 3.4.4
    idna               3.11
    pip                25.2
    requests           2.32.5
    soupsieve          2.8
    typing_extensions  4.15.0
    urllib3            2.5.0
    xlsxwriter         3.2.9
10. run 'stash_graves.py' and 'dig_graves.py'

## Bug fixes / Further development
As mentioned earlier, these scripts were written for a specific project. They are not intended to be an open-source project. Please use them as-is and do not expect on-going support or updates. Hopefully though they will provide you with inspiration for your own versions.
## License
This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

A copy of the GNU General Public License is [included](LICENSE.txt) in this repository. Please also refer to https://www.gnu.org/licenses/.
## About me
You can lern more about the developer at https://dougfoster.me.
