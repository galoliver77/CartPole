# **Invertált inga (Cart-Pole) szimuláció és optimalizáció**

Ebben a projektben egy kocsira szerelt invertált inga (Cart-Pole) matematikai modelljének szimulációját és szabályozását valósítottam meg Python környezetben. A cél egy olyan állapot-visszacsatolt szabályozó paramétereinek meghatározása volt, amely képes az instabil rendszer stabilizálására.

A rendszer numerikus szimulációja Forward Euler integrálással történt, míg a szabályozó erősítési mátrixának optimalizálását gradient descent segítségével végeztem.

A projekt célja nem egy kész szabályozó átvétele volt, hanem annak vizsgálata, hogy egy egyszerű optimalizációs módszerrel milyen mértékben lehet stabil szabályozási paramétereket találni egy nemlineáris, instabil rendszerhez.

## A fizikai modell

A Cart-Pole rendszer differenciálegyenleteinek felírásához szükséges fizikai háttér és modellalkotási képletek a következő szakirodalom alapján készültek:

Irányítási rendszerek elmélete és tervezése — Lantos Béla

A könyvben szereplő mozgásegyenletek alapján építettem fel a szimulációs modellt.

## A rendszer állapottere

A modell az alábbi állapotváltozókat használja:

kocsi pozíció
kocsi sebesség
inga szöge
inga szögsebessége

## A szabályozó bemenet:

u=−Kx

ahol:

x az állapotvektor
K a keresett visszacsatolási mátrix

## Numerikus szimuláció

A rendszer időbeli viselkedésének szimulációja Forward Euler módszerrel történt.

Ennek oka:

egyszerű implementáció
a rendszer dinamikájának jól követhető vizsgálata
gyors iteráció optimalizáció közben

A szimuláció során minden időlépésben kiszámításra kerül:

az aktuális állapot
a szabályozó bemenet
a következő állapot
Optimalizáció – Gradient Descent

A K visszacsatolási mátrix elemeit gradient descent algoritmussal optimalizáltam.

A cél olyan K paraméterek meghatározása volt, amelyek képesek az invertált inga stabilizálására, miközben minimalizálják a rendszer két legfontosabb hibáját:

az inga szöghibáját
a kocsi pozícióhibáját

A veszteségfüggvényt (loss function) ezeknek a hibáknak az alapján definiáltam, vagyis az optimalizáció során azt vizsgáltam, hogy egy adott K mátrix mellett mennyire sikerül:

az ingát függőleges helyzet közelében tartani
a kocsit a kívánt pozíció közelében tartani

Ebben a projektben a sebességállapotok, illetve a szabályozójel nagysága nem szerepeltek külön optimalizációs szempontként; a fókusz kifejezetten a rendszer legfontosabb állapotváltozóinak stabilizálásán volt.

## Többszöri futtatás 

Mivel az optimalizáció minden futtatás elején véletlenszerű kezdeti K mátrixból indul, az algoritmus különböző kiindulási feltételek mellett eltérő megoldásokhoz juthat.

Ezért a projekt során több egymástól független optimalizációs futtatást végeztem, különböző kezdeti K értékekkel.

Ennek célja az volt, hogy megvizsgáljam:

mennyire érzékeny az algoritmus a kezdőfeltételekre
milyen eltérő lokális optimumok jelennek meg
