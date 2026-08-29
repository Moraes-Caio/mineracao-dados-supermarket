# Configurações do Apriori — WEKA

Registro das execuções do algoritmo Apriori sobre `supermarket_filtrado.csv`.

Em parte das análises a coluna `total` foi temporariamente excluída.

---

## Tentativa 1

- lowerBoundMinSupport → 0.1
- upperBoundMinSupport → 0.7
- metricType → Leverage
- minMetric → 0.1
- numRules → 10

Resultado: nenhuma regra encontrada. Métrica mínima alta demais.

---

## Tentativa 2

- lowerBoundMinSupport → 0.3
- upperBoundMinSupport → 0.6
- metricType → Leverage
- minMetric → 0.04
- numRules → 100

Regra forte obtida:

```
biscuits=t vegetables=t 1764 ==> fruit=t 1404
conf:(0.8) lift:(1.24) < lev:(0.06) [274]> conv:(1.76)
```

---

## Tentativa 3

- lowerBoundMinSupport → 0.3
- upperBoundMinSupport → 0.6
- metricType → Lift
- minMetric → 1.25
- numRules → 100

Resultado: nenhuma regra forte encontrada.

---

## Tentativa 4

- lowerBoundMinSupport → 0.3
- upperBoundMinSupport → 0.6
- metricType → Lift
- minMetric → 1.20
- numRules → 100

Regras obtidas:

```
milk-cream=t vegetables=t 2025 ==> fruit=t 1571
conf:(0.78) < lift:(1.21)> lev:(0.06) [274] conv:(1.6)

party snack foods=t 2330 ==> biscuits=t 1592
conf:(0.68) < lift:(1.21)> lev:(0.06) [280] conv:(1.38)
```

---

## Tentativa 5

- lowerBoundMinSupport → 0.1
- upperBoundMinSupport → 0.8
- metricType → Leverage
- minMetric → 0.05
- numRules → 100

Regra forte obtida:

```
bread and cake=t biscuits=t 2083 ==> frozen foods=t 1510
conf:(0.72) lift:(1.23) < lev:(0.06) [286]> conv:(1.5)
```

---

## Tentativa 6

- lowerBoundMinSupport → 0.2
- upperBoundMinSupport → 0.6
- metricType → Leverage
- minMetric → 0.06
- numRules → 200

Regra forte obtida:

```
juice-sat-cord-ms=t biscuits=t 1542 ==> party snack foods=t 1068
conf:(0.69) lift:(1.38) < lev:(0.06) [291]> conv:(1.61)
```
