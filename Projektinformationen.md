
# Informatikprojekt

<details>
  <summary>Inhaltsverzeichnis</summary>
blablli bli blub
</details>


## 1.Einführung
* Sinn des Spiels
* Snap! ist eine blockbasierte Programmiersprache für Einsteiger. Der Vorteil an solchen Programmierumgebungen ist, dass kompliziertere Java Programmierabläufe und commands auf einfacher verständliche Blöcke mit "Beschriftung" heruntergebrochen sind und sie deshalb gut für Einsteiger geeignet sind.
* Ball Hunter ist ein Spiel bei dem der Spieler den Protagonisten "Alien" steuert. Das Ziel dabei ist, in möglichst kurzer zeit so oft, wie möglich den Ball zu fangen. Mit steigendem Spielfortschritt steigt auch der Anspruch und es kommen Herausforderungen auf den Spieler zu. Gewonnen hat der Spieler, wenn es ihm gelungen ist, den Ball 40 mal einzusammeln, ohne dabei von seinem gegner, dem Anti-Alien gefangen zu werden.

## 2.Code
2.1 Grundbefehle
  * Tastenbelegung 
 Mit den Kontrolltasten w,a,s,d,f kann der Spieler das Alien steuern. Mit w geht er vorwärts, mit a und d wechselt er die Blickrichtung und mit s bewegt er sich rückwärts. 
  Im code sind diese Befehle mit einem control Block mit dem jeweiligen input ("when ... is pressed") und einem Motion block (move ... steps, turn ... degrees) umgesetzt.
  
  ![eins](https://user-images.githubusercontent.com/42579272/48915856-820e4d00-ee80-11e8-9027-822efd05e3fc.JPG "w,a,s,d BILDER")

  * Stage
  Die Stage ist ein "noCopyright" Bild eines leicht zerknüllten Blattes, welches den Hintergrund weniger öde wirken lässt, sich aber trotzdem nicht aufdrängt. Vom ästhetischen Effekt abgesehen, hat die Stage keine Bedeutung im Spiel.
2.2 Spielrahmen
  * Anfangsscreen
Zu Beginn des Spiels wird der Spieler durch ein schwarzes Bild aufgefordert, die Leertase ("Space") zu drücken. Der Startbildschirm ist so konzipiert, dass er immer dann angezeigt wird, wenn ein neues Spiel beginnen soll. Er wird also dann angezeigt wenn,
- der spieler gewonnen hat
- der Spieler das grüne "reset" Fänchen gerückt hat
- der Spieler verloren hat (erst nachdem der "Game over" screen abgelaufen ist und den neustart befehl "Press Space" ausgegeben hat)

![screenshot 2018-11-23 19 20 48](https://user-images.githubusercontent.com/42579272/48956727-e8fd3600-ef54-11e8-8881-923a51a31cba.png)

Folgt der Spieler dieser Anweisung, werden diverse "Spielbeginnmechaniken" ausgelöst. Zuerst verschwindet der "Press Space" Bildschirm und der Spieler sieht zum ersten Mal das Spielfeld. Alien wird in die Mitte des Bildschirms teleportiert und fragt den Spieler nach seinem Namen, welchen dieser in einem Textfeld eintragen darf. Ist das geschehen, prüft das Spiel in einer Liste, ob dieser Spielername bereits existiert. Ist das nicht der Fall, wird der Name zur Liste hinzugefügt und der Spieler wird gefragt, ob er schon einmal (z.B. unter einem anderen Namen) gespielt hat. Beantwortet der Spieler die Frage mit Ja wird das Spiel gestartet, beantwortet er die Frage mit Nein, dann durchläuft der Spieler das [Tutorial](#h1).

Im Code ist das verschwinden des "Press Space" durch einen einfachen "if space is pressed" -> "hide" (also wenn die Leertaste gedrückt wird, mach dich unsichtbar) Block gelöst.

![screenshot 2018-11-23 19 38 17](https://user-images.githubusercontent.com/42579272/48957178-58742500-ef57-11e8-867c-3509c8005613.png)

Durch das drücken der Leertaste wird außerdem der Alien in die Mitte des Bildschirms teleportiert und horizontal ausgerichtet. Damit beim drücken der Leertase nicht mitten im Spiel der Alien in die Mitte teleportiert wird, ist eine "if" Voraussetzung vorgeschaltet, die verlangt, dass der Befehl nur dann ausgeführt wird, wenn der Wert der ["score" Variable](#score-Erklärung) "0" ist. 

![screenshot 2018-11-23 19 41 34](https://user-images.githubusercontent.com/42579272/48957265-cddff580-ef57-11e8-8bf0-288b4469013e.png)

  * Tutorial <a name="h1"></a>
  * Game-Overscreen
  
2.3 Bewertungssystem
  * Scoreboard 
  * Punktevergabe/ Listung

2.4 Timer

### 3.Sprites:
* Alien
* Anti-Alien
* Anti-Alien 2 (mini)
* Anti-Alien 3 (mini)
* Random Laufender
* Ball

### 4.Herausforderungen
4.1 Glide-Problematik
  * Scorepunkte
4.2 Steuerungsdefizit
  * a, und d nur Blickrichtung
  

### 5.Fazit
* Ausblick







