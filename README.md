# matlab 101

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

Zum Beispiel lassen sich nur `1.`-Funktionen direkt mit `solve(f)` lösen, nicht jedoch `2.`.

## Analysis

Nullstellen einer Funktion

```
syms x
f = @(x) x^2 - 2
solve(f, x)
```

Ableiten einer Funktion

```
f1 = diff(f, x, 1) % Erste Ableitung
f2 = diff(f, x, 2) % Zweite Ableitung
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
