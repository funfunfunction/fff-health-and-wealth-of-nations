---
title: Rosling test
toc: false
---


```js
const nations = FileAttachment("./data/nations.csv").csv({typed: true});
```

```js

const yearIndex = view(
  Inputs.range(
    [0, rangeYears.length-1],
    {step: 1, label: 'year', format: (x) => rangeYears[x] }
  )
);
```

```js
const year = rangeYears[yearIndex]
```

```js
const lastDefined = {
  reduceIndex(I, X) {
    for (let i = I.length - 1; i >= 0; --i) {
      const x = X[I[i]];
      if (x != null) {
        return x;
      }
    }
  }
}
```


```js

Plot.plot({
  width: 1152,
  height: 600,
  grid: true,
 
   
  x: { type: "log", domain: [200, 100e3] },
  y: { domain: [15, 85], ticks: 8 },
  color: { legend: true },
  marks: [
    Plot.dot(nations, Plot.groupZ({
      x: lastDefined,
      y: lastDefined,
      r: lastDefined,
      fill: "last",
      
    }, {
      filter: (d) => d.year <= year,
      x: "income",
      y: "lifeExpectancy",
      r: "population",
      fill: "region",
      z: "name",
    })),
    Plot.tip(nations, Plot.pointer(Plot.groupZ({
      x: lastDefined,
      y: lastDefined,
      r: lastDefined,
    }, {
      filter: (d) => d.year <= year,
      x: "income",
      y: "lifeExpectancy",
      r: "population",
      z: "name",
      title: (d) => d.name
    })))
  ]
})
```

```js
nations
```

```js
const rangeYears = d3.sort(d3.union(nations.map((d) => d.year, 10)))

```
```js
rangeYears
```