# ChartJS Tips & Tricks

## How to set max width to bars in a bar chart?

In `options > scales > xAxes > CONFIG OBJECT`, set `maxBarThickness` to a number. e.g. `50`. The bar will not exceed that width value in pixels.

https://www.chartjs.org/docs/latest/charts/bar.html?h=maxbarthickness

## How to stop ChartJS from forcing aspect ratio calculation that leads to unusually large graphs?

In `options` set `maintainAspectRatio: false` to render charts without chartjs forcing height values relative to the width used by it.

https://www.chartjs.org/docs/latest/general/responsive.html?h=maintainaspectratio

## How to format the ticks on Y Axis?

Say you get duration in milliseconds but you want to show the ticks on the Y Axis as a duration in hh:mm:ss format. For this, you can

1. Create a function that does the converstion. e.g. `convertMillisToDuration(millis)`
2. Use this function in the ticks callback for yAxes in scales. Example &mdash;

```js
{
  scales: {
    yAxes: [
      {
        ticks: {
          callback(value, index, values) {
            return convertMillisToDuration(value);
          }
        }
      }
    ];
  }
}
```

I have not used the `index` and `values` arguments but they can used too to for ticks like `1/10 Items`.

https://www.chartjs.org/docs/latest/axes/labelling.html#creating-custom-tick-formats

## How to get stacked bar charts?

```js
{
  scales: {
    xAxes: [
      {
        stacked: true
      }
    ],
    yAxes: [
      {
        stacked: true
      }
    ]
  }
}
```

https://www.chartjs.org/docs/latest/charts/bar.html#stacked-bar-chart

## How to get bars of same fill / background colors?

Set the `backgroundColor` property in datasets array as a string representing a color and chartjs will use that color for all bars. Example &mdash;

```js
datasets: [{
  data: [45, 25, 20, 10],
  backgroundColor: "#002665"
}],
```

## How to get bars of different fill / background colors?

Set the `backgroundColor` property in datasets array to an array of strings representing a colors and chartjs will use those colors for the bars that match the same index as of the data array. Example &mdash;

```js
datasets: [
  {
    label: "# of Votes",
    data: [12, 19, 3, 5, 2, 3],
    backgroundColor: [
      "rgba(255, 99, 132, 0.2)",
      "rgba(54, 162, 235, 0.2)",
      "rgba(255, 206, 86, 0.2)",
      "rgba(75, 192, 192, 0.2)",
      "rgba(153, 102, 255, 0.2)",
      "rgba(255, 159, 64, 0.2)"
    ]
  }
];
```

If you don't have a color for a value in `data`, a default color will be used.

## How to remove animations from charts?

### Approach 1

```js
options: {
  animation: false;
}
```

### Approach 2

```js
options: {
  animation: {
    duration: 0;
  }
}
```

> Setting duration to 0 stills allows to use the `options.animation.onComplete()` callback for custom drawings on the chart, when rendering has finished.

https://stackoverflow.com/questions/21389341/disable-animation-with-charts-js
