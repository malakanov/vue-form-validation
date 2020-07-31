<template>
  <div>
    {{ clientForm }}
    {{ $v }}
    <h2>Клиент</h2>
    <div class="field">
      <label for="lastName">Фамилия</label>
      <input
          id="lastName"
          placeholder="Введите фамилию"
          type="text"
          v-model.trim="clientForm.lastName"


      />

    </div>
  </div>
</template>

<script>
export default {
  name: "ClientComponent",
  props: {
    value: {
      type: Object,
    },
    v: {
      type: Object,
    }
  },
  computed: {
    clientForm: {
      get() {
        return this.value;
      },
      set(value) {
        this.v.$touch();
        this.$emit("input", value);
      }
    }
  }
}
</script>

<style scoped>

</style>
