Absolute Series Scanner (ASS):
==============================
Better ABsolute Scanner (BABS) has been replaced by Absolute Series Scanner (ASS), which i have entirely re-written.
I recommend installing the "Absolute Series Scanner" as it supports nearly everything out of the box, normal season numbering, absolute numbering (a requirement with AniDB and anime in general), grouping folders, DVD folders (limited)...

Here are Absolute Series Scanner features:
    * direct matching by putting in the serie (or serie/Extras folder) an *.id file with the series id (anidb, tvdb, tmdb) 
    * direct matching by putting at the end of the serie folder name " [anidb-12345]" or " [tvdb-1234567]" with the sereis id
    * Giving a tvdb id will make the absolute series show with tvdb seasons transparently.
    * Clever episode number detection
    * DVD    folder support (some vob seem protected, pendign feedback on proportion from users)
    * BluRay folder support (some vob seem protected, pendign feedback on proportion from users)
    * Support 

HTTP Anidb Metadata Agent (HAMA)
================================
HAMA was initially created By Atomicstrawberry until v0.4 included.
I have used a date stamp ex 2015-08-31 for the versions

Here are HAMA agent features:

    * AniDB ID to TVDB/TMDB ID matching (with studio and episode mapping list) with ScudLee's xml mapping file
    * Posters from TVDB (assign a poster to each anidb id in anidb to tvdb mapping file to avoid poster duplicates)
    * TVDB episode screenshots
    * Episode summary (in English only) courtesy of TVDB through ScudLee's XML episode mappings
    * Uses studio from mapping file then AniDB (as often missing from AniDB)
    * Search part entirely local through AniDB HTML API database file anime-titles.xml
    * Separate language order selection for the series name and episode titles in Agent Settings (Supports Kanji characters in folders, filenames, titles)
    * Warnings in html report files (no poster available, episode summary empty, TVDB id not in mapping file) to allow the community to update more easily the mapping XML or TVDB, list of missing episodes
    * Collection mapping from ScudLee's movie collection ammended with AniDB RelatedAnime field
    * Unique posters by using the anidbid rank in the mapping to rotate the posters
    * when a serie is not found in AniDB, search TVDB and TMDB automatically
    
Metadata source
===============
I use AniDB HTTP title database file and ScudLee's XML files with his approval

ScudLee's XMLs:                 https://github.com/ScudLee/anime-lists/
ScudLee's XBMC AniDB mod agent: http://forum.xbmc.org/showthread.php?tid=142835&pid=1432010#pid1432010

    * anime-titles.xml        AniDB HTTP API, contain all anime titles, downloaded from http://anidb.net/api/anime-titles.xml.gz
    * anime-list-master.xml   ScudLee's AniDB to TVDB xml mapping file, give studio and episode mapping list for te episode overview, downloaded from [here](https://raw.github.com/ScudLee/anime-lists/master/anime-list-master.xml)
    * anime-movieset-list.xml ScudLee's movie collection (Because XBMC only supports movie collection and the files were developed for AniDB mod XBMC plugin), downloaded from [here](https://raw.github.com/ScudLee/anime-lists/master/anime-movieset-list.xml)

HAMA downloads the XMLs from the internet (using Plex cache for 1 week), then local, then resource folder.
For pictures and theme songs, it takes from the cache first, then the internet

The XMLs are downloaded (cached) and a copy is saved In the agent data folders and used in case of connection issues
    * anime-titles.xml:	         http://anidb.net/api/anime-titles.xml.gz [API: http://wiki.anidb.net/w/API]
    * anime-list-full.xml:	 Maps the AniDB ID to the TVDB ID, providing studio,episode mapping matrix, tmdb/tmdb id
    * anime-movieset-list.xml: 	 Allows movies to be grouped together
    * tvdb benner and serie xml: episode titles and summaries, screenshot, posters
    * anidb serie xml:           Serie information, poster
    * Plex theme song:           Serie theme song

I did change the metadata id from the Anidb ID to "anidb-xxxxx" with xxxxx being the anidbid.
You can use anidb.id file in series or Series/Extras folder or in the serie name " [anidbid-xxxxx]" at the end of serie folder name, works also for tvdb " [tvdb-xxxxxxx]". Older agents before that need to re-create the library to have a metadata.id beginning with "anidb-"

Installation
============

Get the latest zip package in (https://forums.plex.tv/discussion/77636/release-http-anidb-metadata-agent-hama#latest).
Archive folders to copy in Plex main folder:

    * "Scanners"         "Scanners" is the only that has to be created. "Series/Absolute series Scanner.py" goes inside. 
    * "Plug-ins"         Hama agent "Hama.bundle" folder goes inside
    * "Plug-ins support" Agent data folders (com.plexapp.agents.hama/DataItems/Anidb|OMDB|plex|TMDB|TVDB) goes inside
    * "Logs"             "X-Plex-Token.id"      Put from an item view xml the url token inside to have a log per library
                         "no_timestamp"         delete to have timestamps in logs)
                         "keep_zero_size_files" delete to have Plex skip empty files)

Plex main folder location:

    * '%LOCALAPPDATA%\Plex Media Server\'                                        # Windows Vista/7/8
    * '%USERPROFILE%\Local Settings\Application Data\Plex Media Server\'         # Windows XP, 2003, Home Server
    * '$HOME/Library/Application Support/Plex Media Server/'                     # Mac OS
    * '$PLEX_HOME/Library/Application Support/Plex Media Server/',               # Linux
    * '/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/', # Debian,Fedora,CentOS,Ubuntu
    * '/usr/local/plexdata/Plex Media Server/',                                  # FreeBSD
    * '/usr/pbi/plexmediaserver-amd64/plexdata/Plex Media Server/',              # FreeNAS
    * '${JAIL_ROOT}/var/db/plexdata/Plex Media Server/',                         # FreeNAS
    * '/c/.plex/Library/Application Support/Plex Media Server/',                 # ReadyNAS
    * '/share/MD0_DATA/.qpkg/PlexMediaServer/Library/Plex Media Server/',        # QNAP
    * '/volume1/Plex/Library/Application Support/Plex Media Server/',            # Synology, Asustor
    * '/raid0/data/module/Plex/sys/Plex Media Server/',                          # Thecus
    * '/raid0/data/PLEX_CONFIG/Plex Media Server/'                               # Thecus Plex community    

MANDATORY: Go into the agent data folder ("Plug-In Support/Data/com.plexapp.agents.hama/DataItems") and make sure the following folders are all created: (folders are included in Zip archive on thread, i recently added "TVDB/episodes" folder for TVDB screenshots).

    * "AniDB"
    * "Plex"
    * "OMDB"
    * "TVDB"
    * "TVDB/_cache/fanart/original"
    * "TVDB/episodes"
    * "TVDB/fanart/original"
    * "TVDB/fanart/vignette"
    * "TVDB/graphical"
    * "TVDB/posters"
    * "TVDB/seasons"
    * "TVDB/seasonswide"
    * "TVDB/text"

Agents can only write data in data folder as binary objects or as dictionaries, but cannot create folders unfortunately.
Any folder missing will crash the agent when an attempt to write inside is done. That is a Framework issue, all attemps are in try/except structure, to no avail...

I use these folders to cache all pictures, theme songs, since they are not cached by Plex.
This way, even if you recreate the whole Plex anime folder entry, you do not have to download the same file again.

Updating:
=========
If no folder in data was created or data moved there and no new option was added to the agent settings, it will work.
   . Update scanner file with the latest from https://github.com/ZeroQI/Absolute-Series-Scanner/blob/master/Series/Absolute%20Series%20Scanner.py
   . replace agent "_ _init_ _.py" with the latest from https://github.com/ZeroQI/Hama/blob/master/Hama.bundle/Contents/Code/__init__.py
If it doesn't, get latest zip and start from scratch, but no need to delete "Plug-in Support" folder

After restarting Plex servers, the new agent will be loaded and you will find all agents settings in the official framework agent settings window:
   * "Plex > Settings > Server > Agents > TV Shows > HamaTV > Agent settings"

Troubleshooting:
================

If nothing is scanned or episodes are missing, or file or series not geting into the GUI, that is the scanner doing...
Include the following logs then:

Support thread for Scanner: https://forums.plex.tv/discussion/113967/absolute-series-scanner-for-anime-mainly/#latest
Scanner logs:               [...]/Plex Media Server/Logs/Plex Media Scanner.log                       (scanner crash info)
                            [...]/Plex Media Server/Logs/Plex Media Scanner (custom ASS).log          (episodes info)
                            [...]/Plex Media Server/Logs/Plex Media Scanner (custom ASS) filelist.log (library file list)

If files and series are showing in Plex GUI but no metadata is downloaded or some is but no poster, that is the Agent doing
If posters are missing, check that all the data folders are created and the agent is where it should be:

Support thread for agent:   https://forums.plex.tv/discussion/77636/release-http-anidb-metadata-agent-hama#latest
Agent logs:                 [...]/Plex Media Server/Logs/PMS Plugin Logs/com.plexapp.agents.hama.log
Hama specific html logs:    [...]/Plex Media Server/Plug-in Support/Data/com.plexapp.agents.hama/DataItems/AniDB.htm
                            [...]/Plex Media Server/Plug-in Support/Data/com.plexapp.agents.hama/DataItems/TVDB.htm
                            [...]/Plex Media Server/Plug-in Support/Data/com.plexapp.agents.hama/DataItems/themes.htm
                            [...]/Plex Media Server/Plug-in Support/Data/com.plexapp.agents.hama/DataItems/anime-list.htm
                            [...]/Plex Media Server/Plug-in Support/Data/com.plexapp.agents.hama/DataItems/Missing Episodes.htm

To Do (if anybody is motivated)
=====

   * Package of Studio Logos. Will not work on that but somebody else can
	https://forums.plex.tv/discussion/120618/new-studio-logos-for-media-flags-bundle
	https://forums.plex.tv/index.php/topic/77636-release-http-anidb-metadata-agent-hama/?p=451061

   * Package of Theme Songs, as local loading supported (name convention: Data/com.plexapp.agents.hama/DataItems/Plex/anidbid.mp3). Plex use 30s songs but use seasons, so a package of songs capped at 30s should share the same legality. Will not work on that but local loading works
   * Add RSS links to AniDB missing episodes summary ?
