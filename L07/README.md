*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Tic Tac Toe

- Schreibe Das Spiel Tic Tac Toe für die Konsole. 

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

Parsing (Umwandeln von Strings (Nutzereingabe) in ints): 

```Java
Integer.parseInt(str); //Wandelt einen String in einen int um, oder wirft einen Fehler.
```


Try-Catch:

![Try-Catch](trycatch.JPG)

Erfülle folgnde Anforderungen: 

- 2 Spieler können das Spiel Spielen
- Spieler können in der Konsole die Felder mit den Zahlen 1-9 ansteuern
- Falsche eingaben werden mit Try/Cath abgefangen
- Das Feld wird nach jeder Eingabe in der Konsole gezeichnet
- Nutzer erhalten hilfreiche Anweisungen

Beispiele:
```Java
//Leeres Feld:
 | | 
 | | 
 | | 

//Feld im Spiel:

X| |O
 |O|X
 | | 
```

- Sind 3 Steine der gleichen "Sorte" in einer Reihe wird ausgegeben welcher Spieler gewinnt

Optional:

- Schreibe einen BOT, der gegen den Spieler Spielt (z.B. per Random oder sogar entsprechend der jeweiligen Möglichkeiten)

---

Beispiellösung:
```Java

package tictactoe;

import java.util.Scanner;

public class TicTacToe {

	static String[] reiheEins = { "-", "-", "-" };
	static String[] reiheZwei = { "-", "-", "-" };
	static String[] reiheDrei = { "-", "-", "-" };

	static boolean user1 = true;
	static boolean won = false;

	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		ausgabe();
		while (!won) {
			String str = s.nextLine();
			try {
				int feldNr = Integer.parseInt(str);
				if (feldNr > 8 || feldNr < 0)
					throw new Exception();
				else
					feldEingegeben(feldNr);
			} catch (Exception e) {
				System.out.println("Falsche Eingabe");
			}
			if (str.equals("exit")) {
				break;
			}
		}
	}

	public static void feldEingegeben(int feldNr) {
		String userVal = "-";
		if (user1)
			userVal = "X";
		else
			userVal = "0";
		if (feldNr < 3) {
			if (reiheEins[feldNr].equals("-")) {
				reiheEins[feldNr] = userVal;
				user1 = !user1;
			} else {
				System.out.println("Feld schon belegt");
			}
		} else if (feldNr < 6) {
			if (reiheZwei[feldNr - 3].equals("-")) {
				reiheZwei[feldNr - 3] = userVal;
				user1 = !user1;
			} else {
				System.out.println("Feld schon belegt");
			}
		} else {
			if (reiheDrei[feldNr - 6].equals("-")) {
				reiheDrei[feldNr - 6] = userVal;
				user1 = !user1;
			} else {
				System.out.println("Feld schon belegt");
			}
		}
		ausgabe();
		checkIfWon();
	}

	public static void ausgabe() {
		for (String string : reiheEins) {
			System.out.print(string + " | ");
		}
		System.out.println();
		for (String string : reiheZwei) {
			System.out.print(string + " | ");
		}
		System.out.println();
		for (String string : reiheDrei) {
			System.out.print(string + " | ");
		}
		System.out.println();
	}

	public static void checkIfWon() {
		String userWon = "-";
		// Spalten ueberpruefen
		for (int i = 0; i < reiheEins.length; i++) {
			if (reiheEins[i].equals(reiheZwei[i]) && reiheZwei[i].equals(reiheDrei[i])) {
				userWon = reiheEins[i];
				break;
			}
		}
		if (userWon.equals("-")) {
			// Zeilen ueberpruefen
			userWon = zeilenUeberpruefen(reiheEins);
			if (userWon.equals("-")) {
				userWon = zeilenUeberpruefen(reiheZwei);
				if (userWon.equals("-")) {
					userWon = zeilenUeberpruefen(reiheDrei);
					if (userWon.equals("-")) {
						// Schraeg ueberpruefen
						if (reiheEins[0].equals(reiheZwei[1]) && reiheZwei[1].equals(reiheDrei[2])
								|| reiheEins[2].equals(reiheZwei[1]) && reiheZwei[1].equals(reiheDrei[0])) {
							userWon = reiheZwei[1];
						}
					}
				}
			}
		}

		if (!userWon.equals("-")) {
			won = true;
			System.out.println(userWon + " hat das Spiel gewonnen");
		}
	}

	public static String zeilenUeberpruefen(String[] reihe) {
		String userWon = "-";
		if (!reihe[0].equals("-")) {
			String firstElement = reihe[0];
			userWon = firstElement;
			for (int i = 0; i < reihe.length; i++) {
				if (!firstElement.equals(reihe[i])) {
					userWon = "-";
					break;
				}
			}
		}
		return userWon;
	}

}

```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

