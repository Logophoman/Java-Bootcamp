*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Mehrfach verkettete Liste

- Schreibe eine Klasse mit dem Namen ChainList die folgende Objektattribute besitzt:
    - int value
    - ChainList nextObject

> **Funktionsweise:** Bei der mehrfach verketteten Liste zeigt jedes Element der Liste auf das nachfolgende Element der Liste und das Letzte Element der Liste auf **NULL**. Damit man durch alle Elemente der Liste iterieren kann, verwendet man Rekursion (Funktion X ruft sich selbst N mal wieder auf, üblicherweise bis eine Bedingung erfüllt ist).

- Schreibe eine Funktion pushValue() die einen neuen Wert der Liste unten hinzufügt

- Schreibe eine Funktion popValue() die den letzten Wert der Liste unten entnimmt

- Schreibe eine Funktion getValue(int position) die einen Wert an einer bestimmten Stelle der verketteten Liste zurückgibt

- Schreibe eine Funktion getArrayFromList() die die verkettete Liste in ein Array umwandelt und zurückgibt

---


Beispiellösung:
```Java
package mehrfachVerkettet;

public class ChainList {
	int value;
	ChainList nextObject = null;

	public ChainList(int inputValue) {
		this.value = inputValue;
	}

	public void pushValue(int inputValue) {
		// Wir gehen davon aus: Ende der Liste
		if (this.nextObject == null) {
			this.nextObject = new ChainList(inputValue);
		} else {
			this.nextObject.pushValue(inputValue);
		}
	}

	public void popValue() {
		if (this.nextObject.nextObject == null) {
			this.nextObject = null;
		} else {
			this.nextObject.popValue();
		}
	}

	public String getValue(int position) {
		if (position <= 0) {
			return "" + this.value;
		}
		if (this.nextObject == null) {
			return "Die Liste ist nicht lang genug!";
		} else {
			return this.nextObject.getValue(position - 1);
		}
	}
	
	public int[] getArrayFromList() {
		if (this.nextObject == null) {
			return new int[] {this.value};
		} else {
			int[] temp = this.nextObject.getArrayFromList();
			int[] result = new int[temp.length + 1];
			
			result[0] = this.value;
			for (int i = 0; i < temp.length; i ++) {
				result[i+1] = temp[i];
			}
			return result;
		}
	}
}

```
```Java
package mehrfachVerkettet;

public class Tester {

	public static void main(String[] args) {
		ChainList firstList = new ChainList(0);
		for (int i = 0; i < 10; i ++) {
			firstList.pushValue(i + 1);
		}
		
		int[] finalArray = firstList.getArrayFromList();
		
		
		for (int i = 0; i < finalArray.length; i++) {
			System.out.println(finalArray[i]);
		}
		
	}
}

```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

