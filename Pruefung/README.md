*[direkt zum Q&A](#-qa-fragen-und-antworten)*

## **A** Übungsprüfung

![Download Aufgabe](https://github.com/Logophoman/Java-Bootcamp/blob/master/Pruefung/Ubungsprufung.pdf)

![Download Beispiellösung](https://github.com/Logophoman/Java-Bootcamp/blob/master/Pruefung/MauMau.zip)

```Java
package MauMau;

public class Spiel {
    private int spielerAmZug = 1;
    private RealSpieler[] spieler;
    private Kartendeck kartendeck;

    public Spiel(int anzahl){
        kartendeck = new Kartendeck();
        kartendeck.ablegen(kartendeck.ziehen());
        spieler = new RealSpieler[anzahl];
        for (int i = 0; i < spieler.length; i++) {
            spieler[i] = new RealSpieler(kartendeck);
        }
        spielerAmZug = ((int) Math.random() * anzahl) + 1 ;
    }
    public void naechsterZug(){
        System.out.println("Ablage: " + kartendeck.ablageOben().toString());
        System.out.println("Spieler Nr. " + spielerAmZug + " ist am Zug.");
        System.out.println(spieler[spielerAmZug - 1].zeigeHandkarten());
        spieler[spielerAmZug - 1].spielen();
        spielerAmZug++;
        if(spielerAmZug > spieler.length){
            spielerAmZug = 1;
        }
    }

    public boolean beendet(){
        for (int i = 0; i < spieler.length; i++) {
            if(spieler[i].keineKarten()){
                return true;
            }
        }
        return false;
    }
}

```

```Java
package MauMau;

import java.util.ArrayList;

public class Kartendeck {
    private ArrayList<Karte> kartenstapel;
    private ArrayList<Karte> ablage;

    public Kartendeck(){
        kartenstapel = new ArrayList<Karte>();
        ablage = new ArrayList<Karte>();
        for(int i = 7; i <= 14; i++){
            addKarte(new Karte("Herz", i));
            addKarte(new Karte("Pik", i));
            addKarte(new Karte("Karo", i));
            addKarte(new Karte("Kreuz", i));
        }
        ablegen(ziehen());
    }
public Karte ziehen(){
    if(kartenstapel.size() < 1){ //
        while (ablage.size() > 1) { // alles bis auf oberste Ablagekarte
            addKarte(ablage.remove(0));
        }
    }
    return kartenstapel.remove(0);
}

public void ablegen(Karte k){
ablage.add(k);
}
public Karte ablageOben(){
return ablage.get(ablage.size()-1);
}
public void addKarte(Karte k){
    kartenstapel.add((int)(Math.random()*kartenstapel.size()), k);
}
}

```

```Java
package MauMau;

public class Main {
    public static void main(String[] args){
        Spiel spiel = new Spiel(2);
        while(!spiel.beendet()){
            spiel.naechsterZug();
        }
        System.out.println("Spiel beendet.");
    }
}
```

```Java
package MauMau;

import org.w3c.dom.ls.LSOutput;

import java.util.Scanner;
public class RealSpieler extends Spieler {
    Scanner scanner = new Scanner(System.in);
    String userEingabe = "";

    public RealSpieler(Kartendeck spielkarten) {
        super(spielkarten);
    }

    public void spielen() {
        while (true) {
            System.out.println("Wollen Sie eine Karte spielen? j: ja, n: nein");
            userEingabe = scanner.nextLine();
            if (userEingabe.equals("n")) {
                System.out.println("Spieler Nr. " + getSpielerNummer() + " zieht eine Karte ");
                getHandkarten().add(getSpielkarten().ziehen());
                break;
            }
            if (userEingabe.equals("j")) {
                while (true){
                    try {
                        System.out.println("Nummer der Karte?");
                        userEingabe = scanner.nextLine();
                        karteAblegen(Integer.parseInt(userEingabe));
                        break;
                    }catch (Exception e){
                        System.out.println("Ungültige Zahl");
                    }
                }
                break;
            }
            System.out.println("falsche Eingabe");
        }
    }
}
```

```Java
package MauMau;

public class Spiel {
    private int spielerAmZug = 1;
    private RealSpieler[] spieler;
    private Kartendeck kartendeck;

    public Spiel(int anzahl){
        kartendeck = new Kartendeck();
        kartendeck.ablegen(kartendeck.ziehen());
        spieler = new RealSpieler[anzahl];
        for (int i = 0; i < spieler.length; i++) {
            spieler[i] = new RealSpieler(kartendeck);
        }
        spielerAmZug = ((int) Math.random() * anzahl) + 1 ;
    }
    public void naechsterZug(){
        System.out.println("Ablage: " + kartendeck.ablageOben().toString());
        System.out.println("Spieler Nr. " + spielerAmZug + " ist am Zug.");
        System.out.println(spieler[spielerAmZug - 1].zeigeHandkarten());
        spieler[spielerAmZug - 1].spielen();
        spielerAmZug++;
        if(spielerAmZug > spieler.length){
            spielerAmZug = 1;
        }
    }

    public boolean beendet(){
        for (int i = 0; i < spieler.length; i++) {
            if(spieler[i].keineKarten()){
                return true;
            }
        }
        return false;
    }
}
```

```Java
package MauMau;

import java.util.ArrayList;

public abstract class Spieler {
private int spielerNummer;
static int spielerAnzahl = 0;
private static final int STARTKARTEN_ANZAHL = 7;
private Kartendeck spielkarten;
private ArrayList<Karte> handkarten;
//StringBuilder sb = new StringBuilder();

public Spieler(Kartendeck spielkarten) {
    this.spielkarten = spielkarten;         // Initialisieren der übergebenen Parameter
    spielerAnzahl++;                        // beim Anlegen eines Spielers erhöht sich die (globale) Spieleranzahl um 1
    spielerNummer = spielerAnzahl;          // beim Anlegen eines Spielers bekommt dieser eine Spielernummer entsprechend der Spieleranzahl
    handkarten = new ArrayList<Karte>();
    for (int i = 0; i < STARTKARTEN_ANZAHL; i++) {
        ziehen();
    }
}
    public int getSpielerNummer() {
        return spielerNummer;
    }

    public Kartendeck getSpielkarten() {
        return spielkarten;
    }

    public ArrayList<Karte> getHandkarten() {
    return handkarten;
    }

    public String zeigeHandkarten(){
        StringBuilder hand = new StringBuilder();
        for(int i = 0; i < handkarten.size(); i++){
            hand.append(i + ": " + handkarten.get(i).toString() + " | ");
        }
        return hand.toString();
    }

    public void print(){
        System.out.println("Handkarten: " + zeigeHandkarten());
        System.out.println("Ablage: " + spielkarten.ablageOben().getFarbe() + " " + spielkarten.ablageOben().getWert());
    }
    public void ziehen(){
        handkarten.add(spielkarten.ziehen());
    }
    public boolean keineKarten(){
        if(handkarten.size() < 1){
            return true;
        }
        return false;
    }
    public void karteAblegen(int index){
        if(handkarten.get(index) != null){
            if(spielkarten.ablageOben().spielbar((handkarten.get(index)))){
                System.out.println("Spieler Nr. " + spielerNummer + " Legt die Karte " + handkarten.get(index).toString());
                spielkarten.ablegen(handkarten.remove(index));
                return;
            }
        }
        System.out.println("Sie können diese Karte nicht spielen");
        System.out.println("Spieler Nr. " + spielerNummer + " zieht eine Karte ");
        handkarten.add(spielkarten.ziehen());

    }
    public void spielen(){

    }
}
```


## **?! _<small>Q&A</small>_** Fragen und Antworten

Fragen von: [Logophoman](https://github.com/Logophoman) eingepflegt.

#### Frage Eins
Antwort zu Frage Eins...

