*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Hangman


- Schreibe Das Spiel Hangman für die Konsole und mehrere Spieler. 

Benötigte Ressourcen:

Scanner in einer While-Schleife um den User Input abzufangen:

```Java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
            while (true){
                String str = s.nextLine();
                System.out.println(str); //Es wird ausgegeben was der Nutzer eingibt.
                if(str.equals("exit")){
                    break;
            }
        }
    }
}
```

Erfülle folgnde Anforderungen: 

- Mehrere Spieler können das Spiel Spielen
- Spieler können in der Konsole Buchstaben und Wörter eingeben
- Spieler können am Anfang ein Wort eingeben
- Danach können die Anderen Spieler Raten
- Nach jedem Versuch werden die Verbleibenden Versuche angezeigt
- Die Zwischenergebnisse werden nach jeder Runde in der Konsole gezeichnet
- Nutzer erhalten hilfreiche Anweisungen

Optional mit Grafischer Darstellung:


```Java
//Beispiel ausgabe in der Konsole:

-------
|   |
|   0
| /-+-\ 
|   | 
|   | 
|  | | 
|  | | 
|
--------

```
---

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

