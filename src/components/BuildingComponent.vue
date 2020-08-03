<template>
  <div>
     <h2>Шаг {{ step }} из 5</h2>
      {{v.buildingForm.$invalid}}
    <div class="field">
      <label class="label" for="city">Город</label>
      <input
        id="city"
        placeholder="Введите название города"
        type="text"
        v-model.trim="buildingForm.city"
        @blur="v.buildingForm.city.$touch() && v.buildingForm.street.$touch() && v.buildingForm.building.$touch()"
        :class="{ 'error': v.buildingForm.city.$error || !v.buildingForm.city.required}"
      />
      <div class="error-message" v-if="!v.buildingForm.city.required">Это обязательное поле</div>

      <div class="error-message" v-if="v.buildingForm.city.$error">
        <template
          v-if="!v.buildingForm.city.maxLength"
        >Название города не должно превышать {{ v.buildingForm.city.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.buildingForm.city.alpha"
        >Название города должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label class="label" for="street">Улица</label>
      <input
        id="street"
        placeholder="Введите название улицы"
        type="text"
        v-model="buildingForm.street"
        @blur="v.buildingForm.street.$touch()"
        :class="{ 'error': v.buildingForm.street.$error }"
      />

      <div class="error-message" v-if="v.buildingForm.street.$error">
        <template
          v-if="!v.buildingForm.street.maxLength"
        >Название улицы не должно превышать {{ v.buildingForm.street.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.buildingForm.street.alphaNum"
        >Название улицы должно содержать только цифры и буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label class="label" for="building">Дом</label>
      <input
        id="building"
        placeholder="Введите номер дома"
        type="text"
        v-model="buildingForm.building"
        @blur="v.buildingForm.building.$touch()"
        :class="{ 'error': v.buildingForm.building.$error }"
      />
      <div
        class="error-message"
        v-if="v.buildingForm.building.$error"
      >Номер дома должен быть числом, числом с литерой или числом с дробью числа</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BuildingComponent",
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
    buildingForm: {
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
