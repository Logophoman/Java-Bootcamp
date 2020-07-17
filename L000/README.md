*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Min/Max Array


- Schreibe eine Funktion getMax die für ein beliebiges Array das Maximum bestimmt und zurückgibt

- Schreibe eine Funktion getMin die für ein beliebiges Array das Minimum bestimmt und zurückgibt

---

```Java
//Beispiellösung

    static int getMax(int [] Werte){
        int max = Werte[0];

        for (int i = 0; i < Werte.length; i++) {
            if(max < Werte[i]){
                max = Werte[i];
            }
        }
        return max;
    }
    static int getMin(int [] Werte){
        int min = Werte[0];

        for (int i = 0; i < Werte.length-1; i++) {
            if(min > Werte[i+1]){
                min = Werte[i+1];
            }
        }
        return min;
    }

```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

