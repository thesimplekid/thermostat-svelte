<script lang="ts">
  import { Form, Field } from "svelte-forms-lib";

  export var closeTimeSet;
  export var zone_num: number;

  async function sendNewTemp(values) {
    const res = await fetch(
      process.env.BASE_URL + `/addSetTemp?zone_num=${zone_num}`,
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          setTemp: values.setTemp,
          startTime: values.startTime,
        }),
      }
    );

    if (!res) {
      console.log("hi");
      alert(JSON.stringify(values, null, 2));
    }
  }

  const formProps = {
    initialValues: {
      startTime: "12:00",
      setTemp: 0,
    },
    onSubmit: (values) => {
      sendNewTemp(values);
    },
  };
</script>

<style>
</style>

<Form {...formProps}>
  <label for="startTime">Start Time</label>
  <Field name="startTime" type="time" />

  <label for="setTemp">Set Temp</label>
  <Field name="setTemp" type="number" />
  <button type="submit">Submit</button>
  <button type="button" on:click={closeTimeSet}>Close Modal</button>
</Form>
