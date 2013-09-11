iTunesToRhythm
==============

This little piece of insanity is a tool that transfers your ratings and playcounts between various players (iTunes, RhythmBox, and Amarok). Supports two-way synchronization in iTunes Mac, RhythmBox, Amarok, and Windows Media Player

Original source from [here](http://www.esanbock.com/iTunesToRhythm/iTunesToRhythm.html)

I modified it import songs' Added Dates from iTunes to Rhythmbox (only from Linux), just use the option ````--dateadded````
 
<h2>Prerequesites:</h2>
* Rhythmbox, Amarok, Windows Media Player, or iTunes<br />
* Python<br />
* libxml2<br />
* python-libxml2 (Python bindings for libxml2)<br />
* MySQLdb python bindings (If using Amarok)<br />
* pywin32 (If using Windows Media Player)<br />
* appscript (If using iTunes on a Mac)<br />
<br />
If you are running a desktop distribution of linux (such as Ubuntu), you probably already have these installed.<br />

<h2>Execution:</h2>

1. Download the code
2. Move/copy/mount all your music where RhythmBox or Amarok can find them (the folder structure doesn't matter)
3. Import all your music into your new player (amarok or rhythmbox)
4. Copy or mount your "iTunes Music Library.xml" file to linux, if copying from itunes.  If going to/from amarok or rhythm, ignore this step
5. Execute the following command: 
````
iTunesToRhythm.py -w -a iTunes\ Music\ Library.xml ~/.local/share/rhythmbox/rhythmdb.xml
````
6. Manually resolve any ambiguities your are prompted for
7. Enjoy your music

Note: if running this tool on a Mac, iTunes is directly supported by using "itunes" as the source or destination. One could for instance, import from amarok directly into ituns on a Mac. On Windows, Windows Media Player is supported by using "wmp" as the source or destination.

<h2>Examples:</h2>

Copy statistics from RhythmBox to an Amarok mysql database, excluding ratings:
````
iTunesToRhythm.py --noratings -a ~/.local/share/rhythmbox/rhythmdb.xml mysql -s musicserver -d amarok -u amarokuser -p verysecret
````
Copy ratings and playcounts from Amarok to itunes on a Mac
````
iTunesToRhythm.py mysql -s musicserver -d amarok -u amarokuser -p verysecret itunes
````
<h2>Usage:</h2>
````
Usage: iTunesToRhythm [options] <inputfile>|mysql|itunes|wmp <outputfile>|mysql|itunes|wmp

Options:
  -h, --help          show this help message and exit
  -c, --confirm       confirm every match
  -w, --writechanges  write changes to destination file
  -a, --disambiguate  prompt user to resolve ambiguities
  -l, --fastandloose  ignore differences in file names when a file size match is made against a single song. Will not resolve multiple matches
  --noplaycounts  do not update play counts
  --noratings  do not update ratings
  --dateadded  import added date from iTunes to Rhytmbox (Linux only)

  Amarok connection options:
   Options for connecting to an Amarok MySQL remote database

   -s SERVERNAME, --server=SERVERNAME
      host name of the MySQL database server
   -d DATABASE, --database=DATABASE
      database name of the amarok database
   -u USERNAME, --username=USERNAME
      login name of the amarok database
   -p PASSWORD, --password=PASSWORD
      password of the user
````
Speciifying "itunes" will attempt to use a running iTunes instance for synchronization (Mac Only)
