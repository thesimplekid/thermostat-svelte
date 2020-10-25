<script lang="ts">
  export let zone_name: string;
  export let current_temp: number;
  export let zone_number: number;
  export let set_temp: number;
  export let low_set: number;
  export let high_set: number;

  const delayForPost: number = 5000;

  var setTempTimer = null;
  var setHighTimer = null;
  var setLowTimer = null;

  async function changeSetTemp() {
    clearTimeout(setTempTimer);
    setTempTimer = setTimeout(async function () {
      const res = await fetch(
        `http://10.30.30.92:3000/temperatures/updateSetTemp/zone/${zone_number}`,
        {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ set_temp: set_temp }),
        }
      );
    }, delayForPost);
  }

  async function changeLowSet() {
    clearTimeout(setLowTimer);
    setLowTimer = setTimeout(async function () {
      const res = await fetch(
        `http://10.30.30.92:3000/temperatures/updateLowSet/zone/${zone_number}`,
        {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ low_set: low_set }),
        }
      );
    }, delayForPost);
  }

  async function changeHighSet() {
    clearTimeout(setHighTimer);
    setHighTimer = setTimeout(async function () {
      const res = await fetch(
        `http://10.30.30.92:3000/temperatures/updateHighSet/zone/${zone_number}`,
        {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ high_set: high_set }),
        }
      );
    }, delayForPost);
  }
</script>

<style>
  #zoneName {
    margin: 0 auto;
  }

  #zoneNumber {
    margin: 0 auto;
  }

  #setRange {
    text-align: right;
  }

  .setTemp {
    margin: 0 auto;
  }

  .currentTemp {
    text-align: center;
    margin: 0 auto;
  }

  .col-6 {
    width: 50%;
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
            <h1 class="currentTemp">Current Temp</h1>
          </div>
          <div class="row">
            <h1 class="currentTemp">{current_temp}</h1>
          </div>
        </div>
        <div class="col-6">
          <div class="row">
            <h1 class="setTemp">Set Temp</h1>
          </div>
          <div class="row">
            <input
              class="setTemp"
              type="number"
              bind:value={set_temp}
              min={low_set}
              max={high_set}
              on:change={changeSetTemp} />
          </div>
          <div class="row">
            <div class="col-6">
              <p id="setRange">set low</p>
            </div>
            <div class="col-6">
              <p id="setRange">set high</p>
            </div>
          </div>
          <div class="row">
            <div class="col-6">
              <input
                type="number"
                style="width:100%;height:100%;"
                bind:value={low_set}
                on:change={changeLowSet} />
            </div>
            <div class="col-6">
              <input
                type="number"
                style="width:100%;height:100%;"
                bind:value={high_set}
                on:change={changeHighSet} />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
