# file nevek specifikusak es egyertelmuen leiroak legyenek

* **Bad examples**

* `NewScreen`

* **Good examples**

* `DocumentNewScreen`

# Metodusok sorrendje :: Class component eseteben

Cel: Fentrol lefele sorrendben rendezzuk a metodusokat

1. context
2. __constructor
3. Lifecycle metodusok
4. render
5. renderXY
6. egyeb metodusok

# Export default

Alapbol a class soraban legyen, kiveve persze ha Redux connect-et hasznalunk
