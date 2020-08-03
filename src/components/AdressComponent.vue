<template>
  <div>
     <h2>Шаг {{ step }} из 5</h2>
    <div class="field">
      <label class="label" for="index">Индекс</label>
      <input
        id="index"
        placeholder="Введите индекс"
        type="text"
        v-model.trim="adressForm.index"
        @blur="v.adressForm.index.$touch()"
        :class="{ 'error': v.adressForm.index.$error }"
      />
      <div class="error-message" v-if="v.adressForm.index.$error">Индекс должен быть в формате 455000</div>
    </div>
    <div class="field">
      <label class="label" for="country">Страна</label>
      <input
        id="country"
        placeholder="Введите название страны"
        type="text"
        v-model.trim="adressForm.country"
        @blur="v.adressForm.country.$touch()"
        :class="{ 'error': v.adressForm.country.$error }"
      />

      <div class="error-message" v-if="v.adressForm.country.$error">
        <template
          v-if="!v.adressForm.country.maxLength"
        >Название страны не должно превышать {{ v.adressForm.country.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.adressForm.country.alpha"
        >Название страны должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label class="label" for="region">Область</label>
      <input
        id="region"
        placeholder="Введите название области"
        type="text"
        v-model.trim="adressForm.region"
        @blur="v.adressForm.region.$touch()"
        :class="{ 'error': v.adressForm.region.$error }"
      />

      <div class="error-message" v-if="v.adressForm.region.$error">
        <template
          v-if="!v.adressForm.region.maxLength"
        >Название области не должно превышать {{ v.adressForm.region.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.adressForm.region.alpha"
        >Название области должно содержать только буквы в кириллице</template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AdressComponent",
   props: {
    value: {
      type: Object,
    },
    v: {
      type: Object,
      required: true,
    },
    step:{
      type: Number,
      required: true,
    }
  },
  computed: {
    adressForm: {
      get() {
        return this.value;
      },
      set(value) {
        this.v.$touch();
        this.$emit("input", value);
      },
    },
  },
};
</script>

<style scoped>
</style>
