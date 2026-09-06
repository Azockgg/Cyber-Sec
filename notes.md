# Hashcat

Befehl: hashcat --identify hash.txt
identifiziert den Hash und gibt an welcher modus er ist


-a 0 — Straight (Wortlisten-Angriff)
Befehl: hashcat -a 0 hash.txt wortliste.txt

-a 1 — Combinator (zwei Wortlisten verknüpfen)
Befehl: hashcat -a 1 hash.txt links.txt rechts.txt

-a 3 — Brute-Force / Mask (Masken-Angriff)
hashcat -a 3 hash.txt '?u?l?l?l?l?d?d'
hashcat -a 3 hash.txt '?1?1?1?1' -1 '?l?d' --increment

-a 6 — Hybrid Wordlist + Mask (Wort + angehängte Maske)
Befehl:hashcat -a 6 hash.txt wortliste.txt '?d?d?d?d'

-a 7 — Hybrid Mask + Wordlist (Maske + vorangestelltes Wort)
hashcat -a 7 hash.txt '?d?d?d?d' wortliste.txt

-a 9 — Association
hashcat -a 9 hash.txt wortliste.txt -r rules/best64.rule

Maskeen parameter:
?l : Kleinbuchstaben (abcdefghijklmnopqrstuvwxyz)?u : Großbuchstaben (ABCDEFGHIJKLMNOPQRSTUVWXYZ)?d : Ziffern (0123456789)?s : Sonderzeichen ( !"#\$%&'()*+,-./:;<=>?@[\]^_{|}~`)?a : Alle druckbaren Zeichen (Kombination aus ?l, ?u, ?d und ?s)?b : Alle möglichen Bytes (0x00 - 0xff)?h : Hexadezimal klein (0123456789abcdef)?H : Hexadezimal groß (0123456789ABCDEF)



Erweiterte Befele:
hashcat -a 1 --stdout -j 'c$1' -k 'u$!' links.txt rechts.txt

hashcat -a 6 -1 '$€!' star.hashcat jahre_staedte.txt '?1?1?1?1?1?1' --increment --increment-min 4 --increment-max 6 


## Rules
 Groß-/Kleinschreibung (Case)
l alles klein · u alles groß · c capitalize · C invert capitalize · t toggle all · TN toggle an Position N

Nichts / Umkehren
: nichts tun · r Wort umkehren (abc → cba) · d verdoppeln (abc → abcabc) · f reflektieren (abc → abccba)

Anhängen / Voranstellen / Löschen
$X Zeichen X anhängen · ^X Zeichen X voranstellen
[ erstes Zeichen löschen · ] letztes Zeichen löschen
DN Zeichen an Position N löschen · xNM M Zeichen ab Position N ausschneiden

Einfügen / Überschreiben
iNX Zeichen X an Position N einfügen · oNX Zeichen an Position N mit X überschreiben

Rotieren / Verschieben
{ nach links rotieren · } nach rechts rotieren
p N (bzw. pN) Wort N-mal duplizieren

Länge / Kürzen
'N Wort nach N Zeichen abschneiden (truncate)

Ersetzen (substitution)
sXY alle X durch Y ersetzen (z. B. sa@ → alle a werden @)
@X alle Vorkommen von X löschen

Zeichen-basierte Manipulation (positionsweise)
zN erstes Zeichen N-mal duplizieren · ZN letztes Zeichen N-mal duplizieren
LN bitweise Shift links an Position N · RN bitweise Shift rechts
+N / -N ASCII-Wert an Position N erhöhen/verringern

„Leet"-artige und weitere
k erste zwei Zeichen tauschen · K letzte zwei tauschen
*NM Zeichen an Position N und M tauschen


## Wörterlisten
Befehl: hashcat --stdout -a 1 liste1.txt liste2.txt > kombiniert.txt
Kombiniert 2 listen nach reihen folge


Befehl: hashcat --stdout -a 1 -j l -k l list.txt list.txt > staedte.txt
-j = links -j = rechts 
erweitert: hashcat -a 1 --stdout -j 'c$1' -k 'u$!' links.txt rechts.txt > out.txt
erweitert: hashcat --stdout -a 1 wortliste.txt wortliste.txt | awk 'length >= 8' > out.txt

Wörterlisten durchsuchen/Filtern:
grep -E -w -i 'Haus|Maus' wortliste.txt > gefiltert.txt
-w wortende/anfang
-i Kleinschreibung ignorieren

# John the ripper


Daten über datei herausfinden:
file name.txt



PAssendes2John finden:
ls /usr/share/john/*2john*        # Kali/Debian-Paket
oder in der Jumbo-Quellinstallation:
ls /path/to/john/run/*2john*

zip2john Datei > out.txt

