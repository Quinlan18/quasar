<template>
  <div class="q-pa-lg">
    <q-option-group
      v-model="group"
      :options="options"
      color="red"
      :left-label="true"
    >
    </q-option-group>
  </div>
</template>
<script>
export default {
  data () {
    return {
      group: 'op1',
      options: [
        {
          label: 'Option 1',
          value: 'op1'
        },
        {
          label: 'Option 2',
          value: 'op2'
        },
        {
          label: 'Option 3',
          value: 'op3'
        }
      ]
    }
  }
}
</script>
