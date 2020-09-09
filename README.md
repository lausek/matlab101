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
