<script>
  import { scaleLinear } from "d3-scale";
  import { data } from "./data.js";
  import { Graphic, Section, RectangleLayer, PointLayer, Line, XAxis, YAxis } from '@snlab/florence'
  import { Slider } from '@bulatdashiev/svelte-slider';

//$: upperlim = sliderval
let year_range = [-60, 2624];

// BELOW THING WORKS TO ADJUST THE SCALING (replace with slider)
//var i = 1;
//var sliderval = setInterval( increment, 100);
//function increment(){
//    i = i + 1;
//    sliderval = i;
//    console.log(i)
//}

//let sliderval = 2623.93
$: widthscale = scaleLinear()
    .domain([-60, sliderval])
    .range([0, 900]);

//  let widthscale = scaleLinear()
//    .domain([-60, 2623.93])
//    .range([0, 900]);

  let lengthscale = scaleLinear()
    .domain([0, 100])
    .range([0, 250]);
  console.log("googdd")
  let datalen = Object.keys(data).length - 1
</script>

<!-- IDEA:  -->

<div class="graph">
  <div class="title">
    <!-- title/header content goes here -->
    <h1>Pizza</h1>
  </div>
  <div class="main-chart">
asdasdsd
<Slider bind:value={year_range}></Slider> <!--Slider thingy-->

    <!-- main chart -->
    <svg id="chart" width="900" height="300" transform="scale(1,-1)">
      {#each {length:datalen} as _, i}
      
      <g id="filicales">
      <line x1={widthscale(data[i].age_calBP)} y1={lengthscale(data[i]['filicales%'])} x2={widthscale(data[i+1].age_calBP)} y2={lengthscale(data[i+1]['filicales%'])} 
      stroke="green" stroke-width="0.2%" stroke-linejoin="round"/>
      </g>

      <g id="poaceae">
      <line x1={widthscale(data[i].age_calBP)} y1={lengthscale(data[i]['poaceae%'])} x2={widthscale(data[i+1].age_calBP)} y2={lengthscale(data[i+1]['poaceae%'])} 
      stroke="orange" stroke-width="0.2%" stroke-linejoin="round"/>
      </g>

      <g id="nothofagus">
      <line x1={widthscale(data[i].age_calBP)} y1={lengthscale(data[i]['nothofagus%'])} x2={widthscale(data[i+1].age_calBP)} y2={lengthscale(data[i+1]['nothofagus%'])} 
      stroke="purple" stroke-width="0.2%" stroke-linejoin="round"/>
      </g>
      
    {/each}
    </svg>
    <!-- <Slider bind:year_range /> -->

  </div>
</div>

<style>
</style>