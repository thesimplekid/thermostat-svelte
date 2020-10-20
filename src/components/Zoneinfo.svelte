<script lang="ts">
  import { xlink_attr } from "svelte/internal";

  import { Icon } from "proi-ui-icons";
  import { Button } from "proi-ui";
  import { Col, Container, Row, Card } from "sveltestrap";

  export let zone_name: string;
  export let current_temp: number;
  export let zone_number: number;
  export let set_temp: number;
  export let low_set: number;
  export let high_set: number;

  function clicked(): none {
    console.log("button clicked");
  }
</script>

<style>
  #zoneName {
    margin: 0 auto;
  }
  #zoneNumber {
    margin: 0 auto;
  }

  #currentTemp {
    margin: 0 auto;
  }
  #setNum {
    text-align: right;
  }
  #setRange {
    text-align: right;
  }
  .setTemp {
    margin: 0 auto;
  }
  .col-6 {
    width: 50%;
  }
  .col-3 {
    width: 25%;
  }
  .padding-0 {
    padding-right: 0;
    padding-left: 0;
  }
  .row {
    display: flex;
    width: 100%;
  }
  .row::after {
    clear: both;
    content: "";
  }

  .card {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    transition: 0.3s;
  }

  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
  }

  .container {
    padding: 10px 16px;
  }
</style>

<main>
  <div class="card">
    <div class="container">
      <div class="row">
        <h1 id="zoneName">{zone_name}</h1>
      </div>
      <div class="row">
        <h2 id="zoneNumber">Zone Number: {zone_number}</h2>
      </div>
      <div class="row">
        <div class="col-6">
          <div class="row">
            <h1 id="currentTemp">Current Temp</h1>
          </div>
          <div class="row">
            <h1 id="currentTemp">{current_temp}</h1>
          </div>
        </div>
        <div class="col-6">
          <div class="row">
            <h1 class="setTemp">Set Temp</h1>
          </div>
          <div class="row">
            <div class="col-6 padding-0">
              <h1 class="setTemp" id="setNum">{set_temp}</h1>
            </div>
            <div class="col-6">
              <button on:click={clicked}>
                <Icon type="arrowUp" color="red" />
              </button>
              <button on:click={clicked}>
                <Icon type="arrowDown" color="blue" />
              </button>
            </div>
          </div>
          <div class="row">
            <div class="col-3 padding-0">
              <p id="setRange">set low: {low_set}</p>
            </div>
            <div class="col-3">
              <button on:click={clicked}>
                <Icon type="arrowUp" color="red" />
              </button>
              <button on:click={clicked}>
                <Icon type="arrowDown" color="blue" />
              </button>
            </div>
            <div class="col-3 padding-0">
              <p id="setRange">set high: {high_set}</p>
            </div>
            <div class="col-3">
              <button on:click={clicked}>
                <Icon type="arrowUp" color="red" />
              </button>
              <button on:click={clicked}>
                <Icon type="arrowDown" color="blue" />
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
