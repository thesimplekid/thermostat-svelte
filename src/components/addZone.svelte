<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { Form, Field } from "svelte-forms-lib";

  const dispatch = createEventDispatcher();

  const formProps = {
    initialValues: {
      zone_name: "",
      zone_number: 0,
      low_set: 0,
      high_set: 0,
      set_temp: 0,
      sensor_ids: "",
    },
    onSubmit: (values: JSON) => {
      dispatch("submitted", {
        zoneInfo: values,
      });
    },
  };
</script>

<style>
</style>

<Form {...formProps}>
  <label for="zone_name">Zone Name</label>
  <Field name="zone_name" type="text" />
  <br />

  <label for="zone_number">Zone Number</label>
  <Field name="zone_number" type="number" />
  <br />

  <label for="high_set">High Set Temp</label>
  <Field name="high_set" type="number" />
  <br />

  <label for="low_set">Low Set Temp</label>
  <Field name="low_set" type="number" />
  <br />

  <label for="set_temp">Set Temp</label>
  <Field name="set_temp" type="number" />
  <br />

  <label for="sensor_ids">Sensors</label>
  <Field name="sensor_ids" type="string" />
  <br />

  <button type="submit">Submit</button>
</Form>
