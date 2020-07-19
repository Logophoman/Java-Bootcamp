*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** String Array alphabetisch Sortieren

- Schreibe eine Funktion mit dem Namen SortiereStringArray die ein Array vom Typ String akzeptiert und ein alphabetisch sortiertes Array zurückgibt.

- Schreibe eine weitere Funktion mit dem Namen SortiereStringArray (Überladung) die ein Array vom Typ String und eine Variable vom Typ boolean akzeptiert und entsprechend des booleans ein alphabetisch von A-Z oder Z-A sortiertes Array zurückgibt.

---

```Java
//Beispiellösung


public class Sortieren {
    public static void main(String[] args) {

        //Problem: Clown & Clownfisch -> Das kürzere Wort wird nicht richtig gefunden

        String [] Werte = {"Zug", "Banane", "Keks", "Kohle", "Kartoffel", "Tee", "Clown", "Hamster","Clownfische",
                "Pferd", "Pinguin", "Habicht", "Aal", "Frettchen", "Dromedar", "Tiger", "Truthahn", "Chinchilla", "Frosch",
                "Delphin","Killerwale","Affe"};
        String [] Werte4 = {"Zug", "Banane", "Keks", "Frettchen", "Dromedar", "Tiger"};
        String [] Werte3 = SortiereStringArray(Werte);

        for (int i = 0; i < Werte3.length; i++) {
            System.out.println(Werte3[i]);
        }
    }

    public static String [] SortiereStringArray(String [] pruefen){
        String [] ergebnis = new String[pruefen.length];

        int zaehler = 0;

        for (int i = 0; i < pruefen.length; i++) {
            for (int j = 0; j < pruefen.length; j++) {
                if(pruefen[i].toLowerCase().charAt(0) > pruefen[j].toLowerCase().charAt(0)){
                    zaehler++;
                }
                if (pruefen[i].toLowerCase().charAt(0) == pruefen[j].toLowerCase().charAt(0)){
                    for (int k = 0; k < pruefen[i].length(); k++) {
                        try {
                            if(pruefen[i].toLowerCase().charAt(k) > pruefen[j].toLowerCase().charAt(k)){
                                zaehler++;
                                break;
                            }
                            if(pruefen[i].toLowerCase().charAt(k) < pruefen[j].toLowerCase().charAt(k)){
                                break;
                            }
                        }catch (Exception e){
                            break;
                        }
                    }
                }
            }

            ergebnis[zaehler] = pruefen[i];
            zaehler = 0;
        }
        return ergebnis;
    }
}


```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

