*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Float Array Sortieren

- Schreibe eine Funktion mit dem Namen SortiereArray die ein Array vom Typ Float akzeptiert und ein sortiertes Array zurückgibt.

- Schreibe eine weitere Funktion mit dem Namen SortiereArray (Überladung) die ein Array vom Typ Float und eine Variable vom Typ boolean akzeptiert und entsprechend des booleans ein jeweils vom kleinsten-größten oder vom größten-kleinsten Wert sortiertes Array zurückgibt.

- Schreibe eine Funktion getMax die mithilfe der SortiereArray Funktion den Max-Wert eines Arrays ermitelt

- Schreibe eine Funktion getMin die mithilfe der SortiereArray Funktion den Min-Wert eines Arrays ermitelt


---

```Java
//Beispiellösung

    public static int [] SortiereIntArray(int [] pruefen){
        int [] ergebnis = new int[pruefen.length];

        int zaehler = 0;

        for (int i = 0; i < pruefen.length; i++) {
            for (int j = 0; j < pruefen.length; j++) {
                if(pruefen[i] > pruefen[j]){
                    zaehler++;
                }
            }
            ergebnis[zaehler] = pruefen[i];
            zaehler = 0;
        }
        return ergebnis;
    }

```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

