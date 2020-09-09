# matlab 101

## Analysis

Ableiten einer Funktion

```
f1 = diff(f, x, 1) % Erste Ableitung
f2 = diff(f, x, 2) % Zweite Ableitung
```

Integrieren einer Funktion (`a` untere Grenze, `b` obere Grenze)

```
s = integral(f, a, b)
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
