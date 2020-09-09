# matlab 101

Zurücksetzen der Umgebung, Löschen aller Variablen

```
clear
```

## Definieren einer Funktion

1. Prinzipiell muss zwischen der Definition über Symbole

```
syms x
f = x^2
```

2. ... und der Definition als `function_handle` unterschieden werden. 

```
f = @(x) x^2
```

Zum Beispiel lassen sich nur `1)`-Funktionen direkt mit `solve(f)` lösen, nicht jedoch `2)`.

## Plotten

Eine Funktion, die Symbole enthält, muss wie folgt gezeichnet werden

```
fplot(f)
```

Mehrere Plots auf eine Anzeige zeichnen

```
hold on
fplot(f)
fplot(g)
hold off
```

## Analysis

Nullstellen einer Funktion

```
syms x
f = @(x) x^2 - 2
solve(f, x)
```

Minimum einer Funktion (`x0` ist Startpunkt der Suche)

```
minX = fminsearch(f, x0)
minY = f(minX)
```

Ableiten einer Funktion

```
f1 = diff(f, x, 1) % Erste Ableitung
f2 = diff(f, x, 2) % Zweite Ableitung
```

Tangente an einer Stelle `g`, Formel: <img src="https://render.githubusercontent.com/render/math?math=t(x)=\frac{\partial%20f}{\partial%20x}(x_0)(x-x_0)%2Bf(x_0)">

```
df = subs(diff(f, x), x, g);
fplot(df*(x-g) + f(g))    
```

Integrieren einer Funktion (`a` untere Grenze, `b` obere Grenze)

```
s = integral(f, a, b)
```

Taylorentwicklung einer Funktion (`x0` ist Entwicklungspunkt)

```
T = taylor(f, x, 'ExpansionPoint', x0)
```

## Lineare Algebra

Definieren einer Matrix (`,` trennt Spalten, `;` trennt Zeilen)

```
A = [1, 2; 3, 4]
```

Definieren eines Vektors

```
b = [1, 2] % Zeilenvektor (inkompatibel mit A)
b = [1; 2] % Spaltenvektor
```

Lösen eines LGS

```
x = linsolve(A, b)
x = A\b
```

... oder mittels Gleichungen

```
syms x y z l1 l2 l3
eqn1 = 2*x + y + z == 2;
eqn2 = -x + y - z == 3;
eqn3 = x + 2*y + 3*z == -10;
[l1, l2, l3] = solve([eqn1, eqn2, eqn3], [x, y, z])
```

Berechnen der Determinante. *Ist ein LGS lösbar <=> Determinante != 0*

```
det(A)
```

## FAQ

- Was bedeutet `properly vectorize your function`?
```
% Funktioniert nur mit Skalaren
f = @(x) x^2
% Funktioniert mit Vektoren
f = @(x) x.^2
```
