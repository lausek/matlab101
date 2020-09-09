# matlab 101

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
% funktioniert nur mit skalaren
f = @(x) x^2
% funktioniert mit vektoren
f = @(x) x.^2
```
