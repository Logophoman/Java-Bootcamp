*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Würfel

- Schreibe eine Funktion mit dem Namen Wuerfel und dem Rückgabewert int, die eine zufällige Zahl zwischen 1 und 6 mit einer Wahrscheinlichkeit von jeweils 1/6 zurückgibt

- Verändere die Funktion so, dass die Funktion zwei Zahlen als Parameter vom Typ int annimmt. Die Funktion soll dann entsprechend der Zahlen zufällige Zahlen mit einer passenden Zufallsverteilung ausgeben.

> Beispiel: Die Zahlen 4 und 8 werden der Funktion zur Verfügung gestellt. Die Funktion gibt nun zufällig Zahlen zwischen 4 und 8 zurück. Die Wahrscheinlichkeit jeder Zahl ist 1/4

- Schreibe unter der Funkion Wuerfel eine weitere Funktion mit dem Namen Wuerfel und dem Rückgabewert int, die einen int Wert als Parameter annimmt (das heißt Überladung). Wird diese Funktion aufgerufen generiert sie einen Würfel mit entsprechend vielen Seiten deren Werte bei 1 beginnen.

> Beispiel: Die Zahl 32 wird der Funktion zur Verfügung gestellt. Die Funktion gibt nun zufällig Zahlen zwischen 1 und 32 zurück. Die Wahrscheinlichkeit jeder Zahl ist 1/32.

---

```Java

//Beispiellösung

public static void main(String[] args) {
for (int i = 0; i < 1000; i ++) {
System.out.println(würfel());
}
}

public static int würfel() {
int result;

result = (int)(Math.random() * 6) + 1;

return result;
}


/////////////////////////////////////////////////

package einfach;

public class Würfel {

public static void main(String[] args) {
for (int i = 0; i < 1000; i ++) {
System.out.println(würfel());
}
}

public static int würfel() {
int result;

result = (int)(Math.random() * 6) + 1;

return result;
}
}

```


## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

