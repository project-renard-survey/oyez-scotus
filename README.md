# Oyez Bulk Data Archive
An extract of data provided by Oyez's archive of materials from the Supreme Court of the United States. See [oyez.org](https://www.oyez.org).

## Updates
This bulk-data repository is updated periodically.  The most up-to-date information is available at all times using our API URLs.  Each file in this repository has a corresponding API URL which always contains the most up-to-date version of the corresponding file.

![CalVer YYYY.0M.0D](https://img.shields.io/badge/calver-YY.0M.0D-22bfda.svg "Calendar Versioning YYYY.0M.0D") Since the updates are specifically date based, we are tagging significant releases using [CalVer](http://calver.org/) Calendar based Version Numbers.  We tag using YYYY.0M.0D syntax (4 digit year, 2 digit month with 0 padding, 2 digit day with 0 padding).

### Zip Download
The Most Current complete version of the Bulk Data archive is always available here:
https://github.com/free-law-coalition/oyez-scotus/archive/master.zip

You can download Specific Tagged Releases by clicking on the zip links on our release page:
https://github.com/free-law-coalition/oyez-scotus/releases

### Git Clone
You can clone our bulk data repository using the Git Version Control system by cloning our public github url:
https://github.com/free-law-coalition/oyez-scotus.git

The advantage to using the Git method is you can update to the latest version at any time using the `git pull` command.

## Data Format
The files located in this repository are presented in [JSON](https://en.wikipedia.org/wiki/JSON) format which is a simple, easy to parse data format.

JSON (short for **J**ava**S**cript **O**bject **N**otation), has the advantage of being both easy to read by a human, and easy to parse by a large variety of programming languages.

```json
{
    "ID": 15049,
    "name": "Antonin Scalia",
    "href": "https:\/\/api.oyez.org\/people\/antonin_scalia",
    "view_count": 54,
    "first_name": "Antonin",
    "middle_name": null,
    "last_name": "Scalia",
    "name_suffix": null,
    "date_of_birth": -1066935600,
    "place_of_birth": "Trenton, NJ",
    "date_of_death": 1455343200,
    "place_of_death": "Shafter, TX",
    "gender": "Male",
    "ethnicity": "Italian",
    "family_status": "Middle class",
    "mother": "Catherine Panaro",
    "father": "Eugene Scalia",
    "mothers_occupation": null,
    "fathers_occupation": "Professor",
...
```

## Repository Folder Structure
The basic structure of this repository is based on the URL Structure of www.oyez.org and our public API available at api.oyez.org.  

The Public API URL returns the most current version of each file and may be more current than the files in this repository.

### advocates
Metadata about the attorneys who have advocated for parties in cases in the Supreme Court.  Referenced from within case metadata.

* File: `advocates/[name].json`
* Page: `https://www.oyez.org/advocates/[name]`
* API: `https://api.oyez.org/people/[name]`

#### Examples

* Lisa S. Blatt
	* File: `advocates/lisa_s_blatt.json`
	* Page: https://www.oyez.org/advocates/lisa_s_blatt
	* API: https://api.oyez.org/people/lisa_s_blatt
* Anthony A. Yang
	* File: `advocates/anthony_a_yang.json`
	* Page: https://www.oyez.org/advocates/anthony_a_yang
	* API: https://api.oyez.org/people/anthony_a_yang

### cases
Case Information is stored in the **cases** folder.  This includes basic metadata about each case, as well as time-coded transcripts of each available oral argument and opinion announcement.

This folder is subdivided by term year (e.g. 2016), older cases are presented as a range (e.g. 1789-1850 is presented as a single folder).  

Within each year folder is a folder for each case by docket number.  Older cases (such as the aforementioned 1789-1850 collection) may be presented by citation instead of docket number.

Within each case folder is a case.json file containing metadata about the case.  This includes metadata such as citation, timeline of events, parties, advocates, and lower court information.  It also contains listings of Oral Arguments, Opinion Announcements, and Voting breakdown for each Justice where available.

#### Oral Argument Transcripts
If there are Oral Argument Transcripts available for a case, there is a subfolder under the case folder named `oral_argument_audio`.  Within this folder is one or more json files containing the timecoded transcript of each oral argument.

For space concerns, the audio files are not located in this repository, however the transcript json contains the urls where each audio file can be downloaded.  Audio files are available in MP3, OGG and M3U8 audio formats.

Time codes in the transcript are presented as a decimal number of seconds since the beginning of the audio file.

#### Opinion Announcement Transcripts
If there are recorded Opinion Announcement Transcripts available for a case, there is a subfolder under the case folder named `opinion_announcement_audio`

Transcripts are stored in this subfolder in the same format as the Oral Argument Transcripts above.

#### Examples

* Brown v. Board of Education of Topeka
	* Case File: `cases/1940-1955/348us483/case.json`
	* Oyez URL: https://www.oyez.org/cases/1940-1955/347us483
	* API URL: https://api.oyez.org/cases/1940-1955/347us483
* Burwell v. Hobby Lobby Stores
	* Case File: `cases/2013/13-354/case.json`
	* Oyez URL: https://www.oyez.org/cases/2013/13-354
	* API URL: https://api.oyez.org/cases/2013/13-354
	* Oral Argument - March 25, 2014
		* Transcript File: `cases/2013/13-354/oral_argument_audio/23268.json`
		* Oyez Player URL: https://apps.oyez.org/player/#/roberts6/oral_argument_audio/23268
		* API URL: https://api.oyez.org/case_media/oral_argument_audio/23268
	* Opinion Announcement - June 30, 2014 (Part 1)
		* Transcript File: `cases/2013/13-354/opinion_announcement_audio/23233.json`
		* Oyez Player URL: https://api.oyez.org/case_media/opinion_announcement_audio/23233
	* Opinion Announcement - June 30, 2014 (Part 2)
		* Transcript File: `cases/2013/13-354/opinion_announcement_audio/23319.json`
		* Oyez Player URL: https://apps.oyez.org/player/#/roberts6/opinion_announcement_audio/23319
		* API URL: https://api.oyez.org/case_media/opinion_announcement_audio/23319

### courts

Each arrangement of justices that makes up one of the standing courts of the U.S. Supreme Court contains a json file here containing metadata about the seated court.

The file is named based on the last name of the chief justice of that particular court followed by a number indicating the particular arrangement.

#### Example

**Roberts Court (2010-2016)**

* File: `courts/roberts6.json`
* Oyez URL: https://www.oyez.org/court/15151/roberts6
* API URL: https://api.oyez.org/courts/roberts6

### justices

Inside the **justices** folder is a json file containing metadata about each Justice of the U.S. Supreme Court.

The basic format of this file is identical to the format for advocates, though some metadata is only on justices and some metadata is only on advocates.

#### Examples

**Antonin Scalia**

* File: `justices/antonin_scalia.json`
* Oyez URL: https://www.oyez.org/justices/antonin_scalia
* API URL: https://api.oyez.org/people/antonin_scalia

## License Information
![Creative Commons Attribution-NonCommercial 4.0 International License](https://i.creativecommons.org/l/by-nc/4.0/88x31.png "Creative Commons Attribution-NonCommercial 4.0 International License")

All content on oyez.org and other sites and projects maintained by Oyez is released under the [Creative Commons Attribution-NonCommercial 4.0 International License](http://creativecommons.org/licenses/by-nc/4.0/).

"Oyez" is a registered trademark of [Oyez, Inc](https://www.oyez.org/).

Requests for specific licensing terms and other usage questions may be sent to license@oyez.org.
