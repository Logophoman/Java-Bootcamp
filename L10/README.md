*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Vier Gewinnt


- Schreibe Das Spiel 4 Gewinnt für die Konsole und zwei Spieler. 

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


```Java
//Abfangen von ungültigen Nummern

            String str = "";
            while (true) {
                try {
                    int x = Integer.parseInt(s.nextLine());
                    break;
                }catch (Exception e){
                    System.out.println("Ungültige Eingabe");
                }
            }
```


Erfülle folgnde Anforderungen: 

- 2 Spieler können das Spiel Spielen
- Steine "fallen" nach unten, weden direkt unten angezeigt
- Spieler können in der Konsole die Reihen in denen ein Stein eingeworfen wird mit den Zahlen 1-10 ansteuern
- Falsche eingaben werden mit Try/Cath abgefangen
- Das Feld wird nach jeder Eingabe in der Konsole gezeichnet
- Nutzer erhalten hilfreiche Anweisungen

Beispiele:
```Java
//Leeres Feld:
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |

//Feld im Spiel:

 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | | | | | | | | |
 | | | |O| | | | | | |
 | | | |X| |X|O|X| | |
 | |X|O|X|O|O|O|X| | |
```

- Sind 4 Steine der gleichen "Sorte" in einer Reihe wird ausgegeben welcher Spieler gewinnt

---

Beispiellösung:
```Java
package vierGewinnt;

import java.util.Scanner;

public class Main {
	public static Board board;
	public static View view;
	public static int stonesToWin = 4;

	public static Spieler currentPlayer = Spieler.SPIELER1;
	public static GameState gameState;

	public static void main(String[] args) {
		gameState = GameState.RUNNING;

		board = new Board(10, 10);
		view = new View(board);

		view.generateView(board);
		view.show();

		Scanner s = new Scanner(System.in);
		while (true) {
			if (gameState == GameState.WON) {
				break;
			}
			String str = s.nextLine();
			System.out.println(str); // Es wird ausgegeben was der Nutzer eingibt.
			if (str.equals("exit")) {
				break;
			}

			int x = 0;

			boolean gameStillValid = true;

			try {
				x = Integer.parseInt(str);
				if (x < 0 || x >= board.width) {
					throw new Exception();
				}
			} catch (Exception e) {
				gameStillValid = false;
				System.out.println("Ungültige Eingabe");
			}
			if (gameStillValid) {
				continueGame(x);
			}
		}
	}

	public static void continueGame(int x) {
		board.insertStone(x);
		view.generateView(board);
		view.show();

		if (board.checkWin()) {
			System.out.println("Player " + currentPlayer + " has won");
			gameState = GameState.WON;
		}

		switchPlayer();
		if (gameState == GameState.RUNNING) {
			System.out.println("it's " + (currentPlayer == Spieler.SPIELER1 ? "X" : "O")  + "s turn!");
		}
	}

	public static void switchPlayer() {
		currentPlayer = currentPlayer == Spieler.SPIELER1 ? Spieler.SPIELER2 : Spieler.SPIELER1;
	}

}
```
```Java
package vierGewinnt;

public class Board {
	public char[][] data;

	public int width;
	public int height;

	public Board(int xMax, int yMax) {
		data = new char[xMax][yMax];
		width = data.length;
		height = data[0].length;
		initializeBoard();
	}

	public void initializeBoard() {
		for (int xIndex = 0; xIndex < width; xIndex++) {
			for (int yIndex = 0; yIndex < height; yIndex++) {

				data[xIndex][yIndex] = ' ';

			}
		}
	}

	public void insertStone(int x) {
		char currentPlayerString = Main.currentPlayer == Spieler.SPIELER1 ? 'X' : 'O';

		for (int yIndex = 0; yIndex < height; yIndex++) {
			try {
				if (checkCollision(x, yIndex)) {
					data[x][yIndex] = currentPlayerString;
					break;
				}
			} catch (ArrayIndexOutOfBoundsException aioobe) {
				data[x][yIndex] = currentPlayerString;
				break;
			}
		}
	}

	public boolean checkCollision(int x, int y) {
		return data[x][y + 1] != ' ';
	}

	public boolean checkWin() {
		for (int yIndex = 0; yIndex < height; yIndex++) {
			for (int xIndex = 0; xIndex < width; xIndex++) {
				char search = data[xIndex][yIndex];
				if (search != ' ') {
					if (checkPattern(search, 1, 0, xIndex, yIndex) || checkPattern(search, 1, 1, xIndex, yIndex)
							|| checkPattern(search, 0, 1, xIndex, yIndex)
							|| checkPattern(search, -1, 1, xIndex, yIndex)) {
						return true;
					}
				}
			}
		}
		return false;
	}

	public boolean checkPattern(char search, int xOffset, int yOffset, int currentX, int currentY) {
		int lookX = 0;
		int lookY = 0;

		for (int patternIndex = 0; patternIndex < Main.stonesToWin; patternIndex++) {
			lookX = xOffset * patternIndex;
			lookY = yOffset * patternIndex;

			lookX += currentX;
			lookY += currentY;

			if (lookX < 0 || lookX >= this.width || lookY < 0 || lookY >= this.height) {
				return false;
			}
			if (this.data[lookX][lookY] != search) {
				return false;
			}
		}
		return true;
	}
}
```
```Java
package vierGewinnt;

public class View {
	public Spieler spieler = Main.currentPlayer;
	public String[] view;

	public View(Board board) {
		generateView(board);
	}

	public void generateView(Board board) {
		view = new String[board.height];
		
		for (int yIndex = 0; yIndex < board.height; yIndex++) {
			String currentLine = "|";
			for (int xIndex = 0; xIndex < board.width; xIndex++) {
				currentLine += board.data[xIndex][yIndex] + "|";
			}
			view[yIndex] = currentLine;
		}
	}
	
	public void show() {
		for (int lineIndex = 0; lineIndex < view.length; lineIndex++) {
			System.out.println(view[lineIndex]);
		}
	}
}

```
```Java
package vierGewinnt;

public enum Spieler {
	SPIELER1, SPIELER2
}

```
```Java
package vierGewinnt;

public enum GameState {
	RUNNING, WON
}

```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

