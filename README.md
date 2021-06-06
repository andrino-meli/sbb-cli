# Transport info from switzerland on the CLI.
## Command line access to the http://transport.opendata.ch API.
* This programm gets connections from 

## Installation
* Requires python3 (andy maybee some python packages with pip)
* The programm is a single python file and can be installed with:
```bash
    cd ~/.local/bin/
    wget https://raw.githubusercontent.com/andrino-meli/sbb-cli/master/sbb-cli.py
    chmod +x sbb-cli.py
    ln -s sbb-cli.py sbb
    pip3 install dateutil
```

## Example Queries
* one can use `sbb-cli.py` or simply the abbreviation `sbb`
* From station to Station: `sbb -f Bern -t Olten -d 3`
* `sbb -f Genf -t Landesmuseum`
* `sbb -f Bern -t "Zürich, Bahnhofsstrasse 1" -c 14:39 -d 1`
* `sbb -f Luzern -t Zürich -c '17.13.21 14:39 -d 1 --arrival`
Note: A lookup of the location is done first and the "best" location is chosen.  
So if we provide "Zürich" we will end up with "Zürich HB". To give a second 
example "Mosn" will become "Mosnang, Dorf".

## Sample output:
            python3 sbb -f "Apenzell" -t "Ramsei" -d 3
            [1] From: Appenzell (4A) At: 19:00 To: Ramsei At: 23:06 Duration: 4:06:00
            [2] From: Appenzell (3B) At: 19:30 To: Ramsei At: 23:29 Duration: 3:59:00
            [3] From: Appenzell (3B) At: 19:30 To: Ramsei At: 23:30 Duration: 4:00:00
            [4] From: Appenzell (4A) At: 20:00 To: Ramsei At: 23:29 Duration: 3:29:00
            [5] From: Appenzell (4A) At: 20:00 To: Ramsei At: 23:30 Duration: 3:30:00
            [6] From: Appenzell (4A) At: 20:00 To: Ramsei At: 00:06 Duration: 4:06:00

            Connection [3]:
            Station: Appenzell At: 19:30 Platform: (3B) "S 23 1192" Heading to: Gossau SG
            Station: Gossau SG At: 20:20 Platform: (4) "ICN 1538" Heading to: Lausanne
            Station: Olten At: 22:37 Platform: (9) "IR 2388" Heading to: Bern
            Station: Burgdorf At: 23:11 Platform: (4) "S 44 30085" Heading to: Hasle-Rüegsau
            Station: Hasle-Rüegsau At: 23:23 Platform: () "NFB 16585" Heading to: Sumiswald-Grünen

## Ussage
* ussage: sbb [-h] -f FROM -t TO [-c TIME] [-a] [-v VIA] [-d DETAIL]

* if this makes little sense just take a look at the example Queries above.  
  They should explain everything.

* whenever you wonna use a whitespace in an argument you must shell escape it. 
  For most shells this can be done by quoting.

* arguments explained:
    *  -h, --help                   show this help message and exit
    *  -f FROM, --from FROM         Departure station
    *  -t TO, --to TO               Arrival station
    *  -c TIME, --time TIME         Departue time and date (multiple formats 
       should work)
    *  -d CONN, --detail Conn       Detailed information to connection [n]
    *  -v VIA, --via VIA            optinal vias, flag can be used multiple times for multiple vias
    * -a, --arrival                 if time and date correspond to the arrival 
      not departure

## Development
* **your idea is appreciated** - just create an issue or even link a pull 
  request.
* documentation of the API can be found here: 
  <http://transport.opendata.ch/docs.html>
### Things to work on or consider
* the output format can be made mor beatifully and data be presented more 
  nicely. Especially the detailed view. Eg. some sort of top-down flow 
  representing the travel.
* vias could be highlighted. Currently when a via is not a change it is not 
  vissible in the detailed view - but as the user has exp. requested it one 
  might highlight it somehow
* Add a verbose mode displaying every passed station on travel.
* do geo location loockup, eg with: 
  <https://stackoverflow.com/a/41497103/13641055>
* nicer way of inputing date and time: eg. tomorrow at 7pm (use library?)
