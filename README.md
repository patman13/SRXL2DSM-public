
-------------------------------------------------------------------------------------------------------

# SRXL2DSM Software #

Patrick Breidenbach, Germany, 03-2016

![](https://licensebuttons.net/l/by-nd/3.0/de/88x31.png)

Dieses Werk ist lizenziert unter einer
Creative Commons Namensnennung-Keine Bearbeitung 3.0 Deutschland Lizenz.

[http://creativecommons.org/licenses/by-nd/3.0/de/](http://creativecommons.org/licenses/by-nd/3.0/de/)


This work is licensed under a
Creative Commons Attribution-NoDerivs 3.0 Germany License.

[http://creativecommons.org/licenses/by-nd/3.0/de/deed.en](http://creativecommons.org/licenses/by-nd/3.0/de/deed.en)

-------------------------------------------------------------------------------------------------------

## Kurzbeschreibung ##

Konverter für Multiplex SRXL nach Spektrum DSM-TX-Modul

Dieses Programm liest die Daten von SRXL per HW-UART ein, passt die Daten an und
sendet die Daten per Software-UART an ein Spektrum-DSM-Modul.
 
 
## Hardware ##

### Benötigte Teile ###

* DSM-Sendemodul
* Arduino Mini Pro 3,3V
* Duo-LED rot/grün
* 2x Widerstand 220R
* Taster
* Multiplex-Empfänger, der SRXL unterstützt
* Akku (2s-Lipo, z.B. Hacker TOPFUEL ECO-RX 500-2S Pack)
* Schalter zum Abschalten der Versorgungsspannung
* optional: Gehäuse (z.B. Kemo G01B)


### Schaltplan ###

                           .-------------------.      
                           |                   |
          M-Link           |                   |       Spektrum-DSM-Module
           .---.           |                   |              .---.
      Data | o-------------| RX            11  |----------------o | RX
           |   |           |                   |              |   |
      Batt | o-------------| RAW           VCC |----------------o | VCC
           |   |           |                   |              |   |
      GND  | o-------------| GND           GND |----------------o | GND
           '---'           |                   |              '---'
                           |                   |
                           |                   |
                           |                   |
                           |                 5 |----------------------------.
                           |                   |                            |
                           |                   |                            |
                           |                 7 |---------------.            |
                           |                   |               |            |
                           |                 8 |------.        |            |
                           |                   |      |        |            |
                           |                   |     .-.       .-.          |
                           '-------------------'     | |       | |          |
                           Arduino Mini Pro 3.3V     | |220R   | |220R      |
                                                     '-'       '-'          |
                                                      |         |           |
                                                      | red     | green     |
                                                      V ->      V ->      | o
                                                      -         -       |=|>
                                                      |         |         | o
                                                      '---------'           |
                                                           |                |
                                                           |                |
                                                           |                |
                                                          ---              ---

### Pinbelegung der verschiedenen DSM-Module ###

#### Short Range Modul X10EMTX ####

Dieses Modul ist im Sender MLP4DSM verbaut.

Anleitung MLP4DSM: [http://www.e-fliterc.com/ProdInfo/Files/EFLH3000-Manual.pdf](http://www.e-fliterc.com/ProdInfo/Files/EFLH3000-Manual.pdf "Anleitung MLP4DSM")

    .
    |  O    O    O              |
    |  VCC  GND  RX             |
	'---------------------------'
    Ansicht von unten, untere Seite ist Platinenrand

* Betriebsspannung: 3,3V DC
* Baudrate: 131 oder 138 kBaud

Es gibt mindestens zwei Versionen des Moduls, die man optisch nicht unterscheiden kann. Erkennen kann man es an dem Quarz des Senders. Ist ein 4,194 MHz verbaut, erwartet das Modul eine Baudrate von 131 kBaud. Der Wert des Quarz des anderen Moduls ist aktuell nicht bekannt.


#### Full Range Modul X1TXN, X1TXO ####

Dieses Modul ist in den folgenden Sendern verbaut: DX4, DX4e, DX5e, DX6i, HP6DSM und LP5DSM

Anleitung DX4e: [https://www.spektrumrc.com/ProdInfo/Files/SPMR4400-Manual.pdf](https://www.spektrumrc.com/ProdInfo/Files/SPMR4400-Manual.pdf "Anleitung DX4e")

    .
    |                                                        |
    |  O    O    O    O    O    O                            |
    |  O    O    O    O    O    O                            |
    |  RX                  VCC  GND                          | 
	'--------------------------------------------------------'
    Ansicht von unten, untere Seite ist Platinenrand

* Betriebsspannung: 3, V DC
* Baudrate: 125 kBaud


## Flashen der Software auf das Arduino-Board ##

Um das hex-File in das Arduino-Board zu flashen, kann das Tool XLoader verwendet werden.

[http://xloader.russemotto.com/](http://xloader.russemotto.com/ "XLoader")


## Bedienung ##

### Eingabe über Taster ###

   Bindevorgang
   Taster beim Einschalten gedrückt halten bis grüne LED leuchtet. Wenn grüne LED leuchtet Taster loslassen.
   --> grüne LED blitzt (Binden-Vorbereitung)
   Modell für das Binden vorbereiten (Akku anschliessen)
   Taster gedrückt halten (Binden beginnt) bis Modell gebunden ist.

   Recihweitentest:
   Taster im Betrieb für mind. 5s gedrückt halten: Reichweitentest wird gestartet (Taster kann nun losgelassen werden)
   Taster für mind. 5s gedrückt halten: um Reichweitentest zu beenden


###  Meldungen über LEDs ###

     Normaler Betrieb:		grün

     Binden-Vorbereitung:	grün blitzen              *    *   *   *   *   *
                                                       *** *** *** *** *** ***

     Binden:				grün blinken schnell      **  **  **  **  **  **
                                                        **  **  **  **  **  **

     Reichweitentest:		rot blitzen               *   *   *   *   *   *
                                                       *** *** *** *** *** ***

     Fehler:				rot blinken               ****    ****    ****
                                                           ****    ****    ****


## Vorbereitungen an der Fernsteueranlage ##
  
### SRXL Version des Empfängers ###
Es gibt bei Multiplex zwei Versionen des SRXL Protokolls.
(siehe: [http://www.multiplex-rc.de/service/downloads/schnittstellenbeschreibungen.html?eID=dam_frontend_push&docID=4233](http://www.multiplex-rc.de/service/downloads/schnittstellenbeschreibungen.html?eID=dam_frontend_push&docID=4233 "SRXL-MULTIPLEX V2"))

Welche Version der jeweilige Empfänger ausgibt, muss der Anleitung des Empfängers entnommen werden.

**Aktuell wird nur die Version 1 unterstützt.**
                                                     
### SRXL (serielle Servoausgabe) am Empfänder aktivieren ###

* MULTIPLEX Launcher starten
* Unter „Weitere Einstellungen -> Optionen…“ folgenden Menüpunkt auswählen:
„Digitale Servodaten“
* Auf den Button „Übernehmen“ klicken.
* Auf den Button „Daten senden“ klicken.
* Auf den Button „Beenden“ klicken.
* MULTIPLEX Launcher schließen, Empfänger abstecken.


### Kanal-Zuordnung am Sender ###

    | Kanal | Funktion    | Reverse |
    |-------|-------------|---------|
    | 1     | Gas         | nein    |
    | 2     | Querruder   | ja      |
    | 3     | Höhenruder  | nein    |
    | 4     | Seitenruder | ja      |     



