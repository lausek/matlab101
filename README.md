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

## Analysis

Nullstellen einer Funktion

```
syms x
f = x^2 - 2
solve(f)
```

Minimum einer Funktion (`x0` ist Startpunkt der Suche)

```
minX = fminsearch(f, x0)
minY = f(minX)
```

> Die Funktion `fminsearch` kann auf die Hochpunkte erweitert werden indem der Funktionsterm mit -1 invertiert wird.

Minimum einer Funktion mit mehreren Variablen

```
x0 = [0, 0]
[xmin, fval] = fminsearch(@(x) f(x(1), x(2)), x0)
```

Ableiten einer Funktion

```
f1 = diff(f, x, 1) % Erste Ableitung
f2 = diff(f, x, 2) % Zweite Ableitung
```

Partielle Ableitung

```
g = x^2 + y^2
diff(g, x) % dg/dx
diff(g, y) % dg/dy
```

Integrieren einer Funktion (`a` untere Grenze, `b` obere Grenze)

```
s = integral(f, a, b)
```

Taylorentwicklung einer Funktion (`x0` ist Entwicklungspunkt)

```
T = taylor(f, x, 'ExpansionPoint', x0)
```

> Die Ordnung der Entwicklung kann über den Parameter `Order` angegeben werden: `taylor(f, x, 'Order', 10, ...)`

Tangente an einer Stelle `g`, Formel: <img src="https://render.githubusercontent.com/render/math?math=t(x)=\frac{\partial%20f}{\partial%20x}(x_0)(x-x_0)%2Bf(x_0)">

```
df = subs(diff(f, x), x, g);
fplot(df*(x-g) + f(g))    
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

## Plotten

Eine Funktion, die Symbole enthält, muss wie folgt gezeichnet werden

```
fplot(f)
```

Mehrere Plots auf einer Anzeige zeichnen

```
hold on
fplot(f)
fplot(g)
hold off
```

Integral mit Fläche zeichnen

```
f = @(x) -1*x.^3+4*x.^2+-5*x+2
x = linspace(0, 5);
inty = cumtrapz(x,f(x));
plot(x, inty, '-k', 'LineWidth',1)
hold on
patch([x fliplr(x)], [zeros(size(x)) fliplr(inty)], 'g')
hold off
```

Fläche unter der Funktion einfärben

```
f = @(x) -1*x.^3+4*x.^2+-5*x+2
area(f(linspace(-10,10)))
```

Plotten einer Funktion mit zwei Variablen

* Als Mesh

```
syms x y;
f = sin(x) + cos(y)
fmesh(f)
```

* Als Fläche

```
syms x y;
f = sin(x) + cos(y)
fsurf(f)
```

## FAQ

- Was bedeutet `properly vectorize your function`?
```
% Funktioniert nur mit Skalaren
f = @(x) x^2
% Funktioniert mit Vektoren
f = @(x) x.^2
```
