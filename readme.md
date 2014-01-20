# dyfi.py

Yksinkertainen cronjobina ajettava dy.fi domain päivitin

## Lyhyesti

    $ dyfi.py --add
    Käyttäjä: kalle.kayttaja@esimerkk.fi
    salasana: salasana123
    Domain nimi: host.dy.fi
    $ dyfi.py -u

## Nimen lisääminen

    $ dyfi.py --add

ja syötä käyttäjä, salasana ja dy.fi nimi kysyttäessä.

## Muokkaus

    $ dyfi.py --edit

dyfi.py avaa oletus editorin (ympäristömuuttuja $EDITOR) tai 'nano' jos $EDITOR
muuttujaa ei ole asetettu

## Käyttö

dyfi.py on suunniteltu ajettavaksi cronjobina, esim. kerran päivässä. dyfi.py
pitää kirjaa mikä on viimeisin IP osoite sekä milloin nimi on viimeksi 
päivitetty, eikä yritä edes päivittää IP-osoitetta jos edellisestä 
päivityksestä on alle 5 päivää tai koneen IP-osoite ei ole vaihtunut.

cronjob lisätään ajamalla

    $ crontab -e

ja lisäämällä rivit

    @reboot dyfi.py -u
    0 */4 * * * dyfi.py -u

Rivit tarkoittavat sitä, että dyfi päivitys tarkistetaan joka kerta kun kone
käynnistyy, sekä neljän tunnin välein. Voit syöttää minuutti kohtaan minkä 
vain kellonajan, mutta on suositeltavaa, että minuuttiosuus asetetaan 
joksikin satunnaisluvuksi 0 ja 59 välillä, jotta dy.fi palvelimet eivät 
kuormitu, jos vaikka kaikki haluavat päivittää dy.fi nimensä samaan aikaan
tasatuntina. 

On turvallista ajaa päivitysohjelma vaikka kerran tunnissa, sillä se ei ota
yhteyttä dy.fi palvelimiin, kuin sillon, jos se kokee päivityksen
tarpeelliseksi.

Lisätietoja löytyy cronjobien tekemiseen löytyy [crontabin man-sivulta](http://manpages.debian.net/cgi-bin/man.cgi?query=crontab&sektion=5)
tai komentorivillä

    $ man 5 crontab
