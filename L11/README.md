*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Sierpinski-Dreieck Fraktal

Für diese Aufgabe wird die library "prog.jar" von Prof. Eisenbiegler benötigt. Wenn Sie diese bereits in ein beliebiges Projekt importiert haben, müssen Sie nichts mehr vorbereiten. Es dauert allerdings maximal 10 Minuten.

<a href="prog.jar" download>prog.jar herunterladen</a>

Schauen Sie sich zuerst dieses Video an, dort wird die Vorgehensweise sehr schön erläutert:
"https://youtu.be/kbKtFN71Lfs"

---

Beispiellösung:
```Java
package sierpinsikiFractal;

import static prog.Picture.*;

public class ChaosFractal {
    public static Vector2D screenDimensions = new Vector2D(1920, 1020, 0);
    public static int[][] defaultPicture = screenDimensions.getDataAsArray();
    public static Vector2D a;
    public static Vector2D b;
    public static Vector2D c;
    public static Vector2D randomPoint;

    public static void main(String[] args) {
        defineCorners(-300);

        drawSierpinski(-300, 1000000);


        show(defaultPicture);

    }

    public static void defineCorners(int color) {
        a = new Vector2D(1, screenDimensions.y - 1, color);
        b = new Vector2D(screenDimensions.x - 1, screenDimensions.y - 1, color);
        c = new Vector2D(screenDimensions.x / 2, 1, color);

        a.draw(defaultPicture);
        b.draw(defaultPicture);
        c.draw(defaultPicture);
    }

    public static void drawSierpinski(int _color, int _maxIteration) {
        randomPoint = new Vector2D(50, 200, _color);
        Vector2D oldVector = randomPoint;
        for (int i = 0; i < _maxIteration; i++) {
            int random = (int) (Math.random() * 3);
            Vector2D pickedVector;
            Vector2D connectionVector;
            Vector2D newVector;


            switch (random) {
                case 0:
                    pickedVector = a;
                    break;
                case 1:
                    pickedVector = b;
                    break;
                case 2:
                    pickedVector = c;
                    break;
                default:
                    pickedVector = a;
                    break;
            }
            connectionVector = oldVector.getConnectionTo(pickedVector);
            Vector2D halfVector = connectionVector.multiplyVector(1f / 2f);
            newVector = oldVector.getAdded(halfVector);
            newVector.draw(defaultPicture);
            oldVector = newVector;
        }


    }
}


```

```Java
package sierpinsikiFractal;

public class Vector2D {
    public double x;
    public double y;
    public int farbe;

    public Vector2D(double _x, double _y, int _c) {
        this.x = _x;
        this.y = _y;
        this.farbe = _c;
    }
    public int[][] getDataAsArray() {
        return new int[(int) this.x][(int) this.y];
    }
    public Vector2D getAdded(Vector2D _passedVector){
        return new Vector2D(this.x + _passedVector.x, this.y + _passedVector.y, this.farbe);
    }
    public Vector2D getSubtracted(Vector2D _passedVector){
        return new Vector2D(this.x - _passedVector.x, this.y - _passedVector.y, this.farbe);
    }
    public Vector2D multiplyVector(double _multiplier){
        return new Vector2D(this.x * _multiplier, this.y * _multiplier, this.farbe);
    }

    public void draw(int[][] _defaultPicture) {
        _defaultPicture[(int) this.x][(int) this.y] = this.farbe;
    }

    public Vector2D getConnectionTo(Vector2D _b) {
        Vector2D routeBetween = _b.getSubtracted(this);

        return routeBetween;
    }

}
```

## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

