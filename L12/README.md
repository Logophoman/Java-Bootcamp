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

```Java
//Beispiellösung

package bootcampss20;

import java.util.ArrayList;
import java.util.Scanner;

public class Hangman {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.println("Herzlich willkommen beim Spiel Hangman.");
        System.out.println("Gib das Geheime Wort ein");
        String str = s.nextLine();
        System.out.println("Um das Spiel zu beenden gib einfach exit ein");
        String geheimwort = str.toLowerCase();
        int versucheÜbrig = 8;

        String ausgabe = "";
        for (int i = 0; i < geheimwort.length(); i++) {
            ausgabe += "_ ";
        }

        ArrayList<Character> gefundeneBuchstaben = new ArrayList<Character>();

        while (true){
            System.out.println(ausgabe);
            System.out.println("Du hast noch " + versucheÜbrig + " Versuche übrig");
            System.out.println("Gib einen Buchstaben ein:");
            str = s.nextLine().toLowerCase();
            char eingabe = str.charAt(0);


            ausgabe = "";
            boolean buchstabeFound = false;
            for (int i = 0; i < geheimwort.length(); i++) {
                if(geheimwort.charAt(i) == eingabe){
                    gefundeneBuchstaben.add(geheimwort.charAt(i));
                    buchstabeFound = true;
                    break;
                }
            }
            if (!buchstabeFound){
                versucheÜbrig--;
                System.out.println("Ätsch! Buchstabe " + eingabe + " kommt nicht vor.");
            }
            int leereBuchstaben = 0;
            boolean matchFound = false;
            for (int i = 0; i < geheimwort.length(); i++) {
                for (int j = 0; j < gefundeneBuchstaben.size(); j++) {
                    if(gefundeneBuchstaben.get(j) == geheimwort.charAt(i)){
                        ausgabe += geheimwort.charAt(i) + " ";
                        matchFound = true;
                    }
                }
                if(!matchFound) {
                    ausgabe += "_ ";
                    leereBuchstaben++;
                }
                matchFound = false;
            }

            if (leereBuchstaben == 0){
                System.out.println("Spiel Gewonnen!");
                break;
            }

            if(str.equals("exit")){
                break;
            }

            if(versucheÜbrig == 0){
                System.out.println("Spiel Verloren!");
                break;
            }
        }
    }
}


```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

