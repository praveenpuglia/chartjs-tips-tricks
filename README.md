# ChartJS Tips & Tricks

## How to set max width to bars in a bar chart?
In `options > scales > xAxes > CONFIG OBJECT`, set `maxBarThickness` to a number. e.g. `50`. The bar will not exceed that width value in pixels.
https://www.chartjs.org/docs/latest/charts/bar.html?h=maxbarthickness

## How to stop ChartJS from forcing aspect ratio calculation that leads to unusually large graphs?
In `options` set `maintainAspectRatio: false` to render charts without chartjs forcing height values relative to the width used by it.
https://www.chartjs.org/docs/latest/general/responsive.html?h=maintainaspectratio

## How to format the ticks on Y Axis?
Say you get duration in milliseconds but you want to show the ticks on the Y Axis as a duration. For this, you can
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
    ]
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
Ref - https://www.chartjs.org/docs/latest/charts/bar.html#stacked-bar-chart
