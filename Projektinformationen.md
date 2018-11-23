
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
 #### Tastenbelegung 

Mit den Kontrolltasten w,a,s,d,f kann der Spieler das Alien steuern. Mit w geht er vorwärts, mit a und d wechselt er die Blickrichtung und mit s bewegt er sich rückwärts. Drückt der Spieler f, kann er sich auf eine zufällige Stelle auf der Map teleportieren, diese Fähigkeit funktioniert allerdings nur 3x, siehe ["Flash"](#flash). 

Im code sind diese Befehle mit einem control Block mit dem jeweiligen input ("when ... is pressed") und einem Motion block (move ... steps, turn ... degrees) umgesetzt.
  
  ![eins](https://user-images.githubusercontent.com/42579272/48915856-820e4d00-ee80-11e8-9027-822efd05e3fc.JPG "w,a,s,d BILDER")
  
  #### Flash
damit der flash Befehl nur 3x funktioniert, wird immer, wenn f gedrückt wird +1 zur Variable "flash" hinzugefügt. Aufgrund eines "if-blocks" wird der "goto" "random position" Block nur dann aktiviert, wenn der flash counter kleiner ist, als 3. Nach dem 3. Einsatz der teleportation ist der Wert für "flash" 3, wodurch der goto random position Block nicht mehr beim drücken von "f" ausgelöst wird.
  
![screenshot 2018-11-23 20 39 57](https://user-images.githubusercontent.com/42579272/48958648-e3a5e880-ef60-11e8-88a7-785f9a587db0.png)


  #### Stage
  
  Die Stage ist ein "noCopyright" Bild eines leicht zerknüllten Blattes, welches den Hintergrund weniger öde wirken lässt, sich aber trotzdem nicht aufdrängt. Vom ästhetischen Effekt abgesehen, hat die Stage keine Bedeutung im Spiel.
2.2 Spielrahmen
 #### Anfangsscreen
  
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

Mit drücken der Leertaste werden außerdem alle anderen Sprites an einen Ort außerhalb der für den Spieler erreichbaren Map teleportiert. Das ist wichtig, damit der Spieler nicht zu Beginn mit zu vielen Reizen, die für Tutorial und Spielbeginn unwichtig sind konfrontiert wird, ist aber _vor allem_ dann wichtig, wenn das Spiel begonnen hat, weil der Spieler, wenn diese nicht vor Spielbeginn wegteleportiert worden wären, mit _noch_ unsichtbaren [Gegnern](#Gegner) kollidieren könnte, was zu einer unfairen Niederlage für den Spieler führen würde. Auch diese hide und teleportationsbefehle funktionieren aus o.g. Gründen nur, wenn "score=0" wahr ist.

![screenshot 2018-11-23 19 50 37](https://user-images.githubusercontent.com/42579272/48957597-d5a09980-ef59-11e8-880a-9e681f164313.png)

Um herauszufinden, ob der Spieler schon einmal gespielt hat und erfahrenen Spielern das Tutorial zu ersparen wird durch das drücken von Space außerdem ein "if, else" control block in gang gesetzt. Zuerst wird der Spieler mit einem "ask" sensing block nach seinem Namen gefragt und hat aufgrund der Beschaffenheit des Blockes die Möglichkeit, eine Antwort einzugeben. "if" (wenn) diese Antwort in der [Spielerliste](#Spielerliste) vorhanden ist, wird der bekannte Spieler begrüßt und ein broadcast-block gibt den Befehl für den [Spielbeginn](#Spielbeginn) aus.

![screenshot 2018-11-23 20 02 51](https://user-images.githubusercontent.com/42579272/48957725-c8d07580-ef5a-11e8-96aa-9d485b50a3eb.png)

steht der eingegebene Name nicht auf der Liste, wird die "else" Seite des Blocks aktiviert, welche dafür sorgt, dass Alien sagt: "Hast du schonmal gespielt?"

![screenshot 2018-11-23 20 06 41](https://user-images.githubusercontent.com/42579272/48957791-544a0680-ef5b-11e8-984e-b7c99ced82be.png)

Daraufhin sendet ein Broadcaster-Block "hast du schonmal gespielt", was zwei Sprites, einer mit einem grünen Haken für "Ja" und ein anderer mit einem roten kreuz für "nein" erscheinen lässt. Auch ein Spieler für den es nicht das erste Mal im Spiel ist hat so die Möglichkeit mit einem neuen Namen anzutreten, denn wenn der Haken angeklickt wird, startet ein Broadcaster-Block das Spiel indem er "start game" ausgibt und so den [Spielbeginn](#Spielbeginn) auslöst.

![screenshot 2018-11-23 20 13 12](https://user-images.githubusercontent.com/42579272/48957924-39c45d00-ef5c-11e8-88a6-7b47e90a882c.png)

Wird das rote X gedrückt, gibt ein Broadcaster "start tutorial" aus und das [Tutorial](#Tutorial) für Neuankömmlinge wird gestartet.

![screenshot 2018-11-23 20 16 12](https://user-images.githubusercontent.com/42579272/48958008-a2133e80-ef5c-11e8-9475-7fb985dc2222.png)

#### Spielerliste <a name="Spielerliste"></a>

In der Spielerliste werden die Namen aller Spieler gespeichert, die das Spiel gespielt und Ihren Namen eingetragen haben. Wird das Spiel lokal gespeichert, erkennt es die Spieler wieder und begrüßt sie zurück. Die Spielerliste wurde als Variable erstellt, um diesem Zweck zu dienen und wird dem Spieler nicht angezeigt. Die Variable wurde mit dem "set to" Block zu einer Liste umgewandelt.

![screenshot 2018-11-23 20 24 50](https://user-images.githubusercontent.com/42579272/48958206-e0f5c400-ef5d-11e8-9d11-e40adeec75b1.png)

#### Spielbeginn <a name="Spielbeginn"></a>

Das Spiel beginnt, wenn ein Broadcaster-Block "Start Game" ausgibt. Dies kann passieren, wenn
- der Spieler das Tutorial beendet hat
- der Spieler seinen bereits bekannten Namen eingibt
- der SPieler einen neuen Namen eingibt, aber mit dem grünen Haken bestätigt, dass er mit den Spielmechaniken bereits vertraut ist.
Wird "Start Game" signalisiert, spielen viele Prozesse gleichzeitig bei unterschiedlichen Sprites ab:

Der ["Ball"](#Ball) wechselt, wenn er "Start Game" empfängt zu seinem Standard-Kostüm, setzt seine Größe zur Normalgröße zurück, beendet die Unsichtbarkeit und begibt sich auf eine zufällige Position auf der Map.

![screenshot 2018-11-23 20 29 54](https://user-images.githubusercontent.com/42579272/48958360-c112d000-ef5e-11e8-8931-4423dcda8b1d.png)

"Alien" wechselt ebenfalls zur neutralen Ausgangsposition, wenn es "Start Game" empfängt. Außerdem setzt der Block die Variable für "flash" auf 0, um dem Spieler zu Beginn jedes Spiels 3 Teleportationen freizuschalten.

![screenshot 2018-11-23 20 32 28](https://user-images.githubusercontent.com/42579272/48958531-f370fd00-ef5f-11e8-80be-5245b3703f12.png)

Ein control block, der sich so lange wiederholt, bis der score den Wert 41 erreicht, beginnt wenn er "start game" empfängt einen sekundenzähler zu simulieren, indem er zur Variable "Zeit" mit dem Abstand von einer sekunde den Wert 1 hinzufügt. Der Wert von 41 wurde gewählt, damit die Uhr zurückgesetzt werden kann, ohne dass der ["Spieler gewinnt"](#Spieler-gewinnt).

![screenshot 2018-11-23 20 55 04](https://user-images.githubusercontent.com/42579272/48958988-be19de80-ef62-11e8-8b25-45083a709138.png)



  #### Tutorial <a name="h1"></a>
  
  Erhält der "Tutorial" Block "start Tutorial", spielt er das tutorial ab. In diesem werden zunächst einige Textnachrichten als Einfühung und Kontextualisierung zum Spiel abgespielt. Gleichzeitig zum Tutorial werden auch einige Spielrelevante objekte, wie zum Beispiel der zu fangende Ball eingeblendet. Um dies zu realisieren wird "tutorial Ball" durch einen broadcast-Block asugegeben. Ein Block im Ball-Sprite empfängt das Signal und blendet den Ball im default Kostüm mit der Standard-Größe so lange ein, wie er im Tutorial erwähnt wird. Danach verschwindet er wieder.
  
  ![screenshot 2018-11-23 21 10 01](https://user-images.githubusercontent.com/42579272/48959197-27e6b800-ef64-11e8-8c91-229f045e0498.png)
  ![screenshot 2018-11-23 21 08 55](https://user-images.githubusercontent.com/42579272/48959176-0685cc00-ef64-11e8-8d21-166c9b957b7c.png)
  
  Im weiteren Verlauf des Tutorials wird dem Spieler die Steuerung des Aliens erklärt. Er wird dann dazu aufgefordert, diese auszuprobieren. Mit Variablen, die erhöht werden, wenn der Spieler die tasten verwendet, die zum Steuern des Aliens benötigt werden, wird aufgezeichnet, welche der Steuerungselemente der Spieler nutzt:
  
  ![screenshot 2018-11-23 21 12 57](https://user-images.githubusercontent.com/42579272/48959275-91ff5d00-ef64-11e8-96ae-aa541b7bda1e.png)
  
  Ein control-Block mit einer "if-clause" überprüft dauerhaft, ob alle Steuerungsvariablen (flash, tut1, tut2, tut3) mindestens einmal erhöht wurden. Er überprüft also, ob der Spieler alle Steuerungselemente mindestens einmal ausprobiert hat. Ist dies nicht der Fall, wird der Spieler, wenn eine der Tutorialvariablen noch 0 ist, dazu aufgefordert, die Steuerung auszuprobieren. Dieser Block wird durch einen "repeat until" Block so lange wiederholt, bis alle Tutorialvariablen größer sind als 0, was bedeutet, dass der Spieler alle Steuerungstasten mindestens einmal ausprobiert hat.
  
  ![screenshot 2018-11-23 21 15 38](https://user-images.githubusercontent.com/42579272/48959392-4a2d0580-ef65-11e8-8711-d75846d3a88d.png)
  
  Wenn diese schleife also beendet ist, weil der Spieler die Steuerung ausprobiert hat und somit auch alle tutorialvariabeln größer, als null sind, was nochmal durch einen "if-Block" überprüft wird, wird das tutorial fortgesetzt und weiterer text ausgegeben. In einem ähnlichen Verfahren wie beim Ball wird der Gegner "Anti-alien" vorgestellt. Daraufhin wird "start game" per broadcast-Block ausgegeben und die Tutorialvariablen werden auf 0 zurückgesetzt.
  
  ![screenshot 2018-11-23 21 20 39](https://user-images.githubusercontent.com/42579272/48959572-90cf2f80-ef66-11e8-94d5-7250f13e2dff.png)
  
  #### Game Over Screen
  Wenn der Game Over Screen "Spieler verliert" empfängt zeigt er sich, um dem Spieler zu signalisieren, dass dieser verloren hat. Er setzt außerdem den Wert des scores auf "41", was den zuvor erklärten "Sekundenzeiger" anhält. Nach 8 Sekunden signalisiert er "Press Space" was das Spiel so in den Ursprungszustand versetzt, wie die grüne Fahne es tun würde, weil "press Space" einer der "reset" Signale ist. Zuletzt verschwindet der Game over screen wieder um das spiel nicht zu überdecken.
  
  ![screenshot 2018-11-23 21 37 13](https://user-images.githubusercontent.com/42579272/48959790-0daed900-ef68-11e8-828c-2af4702a4515.png)
  
  #### score <a name="score"></a> <a name="score-Erklärung"></a>
  "score" ist eine Variable, welche dem Spieler nach Spielbeginn angezeigt wird. Sie wird erhöht, wenn es dem Spieler gelingt, denn Ball einzusammeln/zu berühren. Bei einem score von 40 hat der Spieler das Spiel gewonnen, siehe [Spieler gewinnt](#Spieler-gewinnt)
  
  
  #### Spieler gewinnt <a name="Spieler-gewinnt"></a>
Der Spieler gewinnt wenn die "score" Variable den Wert 40 erreicht hat. Die "score" Variable wird immer dann erhöht, wenn "Alien" "Ball" berührt. Mehr dazu in [score](#score). Hat der score den Wert 40 wird der ein Block aktiviert, welcher dem Spieler gratuliert. Danach wird der bereits erwähnte Sekundenzeiger angehalten, indem zur variable "score" 1 hinzugefügt wird, nachdem diese versteckt wurde, um zu verhindern, dass der Spieler vorgänge im Hintergrund bemerkt. Dem Spieler wird daraufhin die Zeit in Sekunden aufgelistet, indem die "Zeit" variable angezeigt wird. Danach gibt ein Broadcaster "Spieler gewinnt" aus, was einer der "reset" Signale ist, wodurch das Spiel für eine neue Runde in den Grundzustand versetzt wird. So, als ob man die Grüne Fahne drücken würde.

![screenshot 2018-11-23 21 50 24](https://user-images.githubusercontent.com/42579272/48960001-d50fff00-ef69-11e8-9b2d-2b3a1c166b63.png)
![screenshot 2018-11-23 21 50 28](https://user-images.githubusercontent.com/42579272/48960003-d7725900-ef69-11e8-8413-57363d476e20.png)
![screenshot 2018-11-23 21 51 38](https://user-images.githubusercontent.com/42579272/48960028-07216100-ef6a-11e8-9581-f0cafbe81cda.png)


### 3.Sprites:
* Alien <a name="Spielerliste"></a>
* Ball
* Anti-Alien
* Anti-Alien 2 (mini)
* Anti-Alien 3 (mini)
* Random Laufender

### 4.Herausforderungen
4.1 Glide-Problematik
  * Scorepunkte
4.2 Steuerungsdefizit
  * a, und d nur Blickrichtung
  

### 5.Fazit
* Ausblick







