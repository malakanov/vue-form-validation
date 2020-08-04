<template>
  <div>
    <div class="field">
      <label class="label" for="lastName">Фамилия</label>
      <input
        id="lastName"
        placeholder="Введите фамилию"
        type="text"
        v-model.trim="clientForm.lastName"
        @blur="v.clientForm.lastName.$touch() && v.clientForm.middleName.$touch() "
        :class="{ 'error': v.clientForm.lastName.$error || !v.clientForm.lastName.required }"
      />
      <div class="error-message" v-if="!v.clientForm.lastName.required">Это обязательное поле</div>
      <div class="error-message" v-if="v.clientForm.lastName.$error">
        <template
          v-if="!v.clientForm.lastName.maxLength"
        >Длина фамилии не должна превышать {{ v.clientForm.lastName.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.clientForm.lastName.alpha"
        >Должна состоять только из букв в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label class="label" for="firstName">Имя</label>
      <input
        id="firstName"
        placeholder="Введите имя"
        type="text"
        v-model.trim="clientForm.firstName"
        @blur="v.clientForm.firstName.$touch()"
        :class="{ 'error': v.clientForm.firstName.$error || !v.clientForm.firstName.required }"
      />
      <div class="error-message" v-if="!v.clientForm.firstName.required">Это обязательное поле</div>
      <div class="error-message" v-if="v.clientForm.firstName.$error">
        <template
          v-if="!v.clientForm.firstName.maxLength"
        >Длина имени не должна превышать {{ v.clientForm.firstName.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.clientForm.firstName.alpha"
        >Должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label class="label" for="middleName">Отчество</label>
      <input
        id="middleName"
        placeholder="Введите отчество"
        type="text"
        v-model.trim="clientForm.middleName"
        @blur="v.clientForm.middleName.$touch()"
        :class="{ 'error': v.clientForm.middleName.$error }"
      />
      <div class="error-message" v-if="v.clientForm.middleName.$error">
        <template
          v-if="!v.clientForm.middleName.maxLength"
        >Длина отчества не должна превышать {{ v.clientForm.middleName.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.clientForm.middleName.alpha"
        >Должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label class="label" for="birthday">Дата рождения</label>
      <input
        id="birthday"
        type="date"
        v-model="clientForm.birthday"
        @blur="v.clientForm.birthday.$touch()"
        :class="{ 'error': v.clientForm.birthday.$error || !v.clientForm.birthday.required }"
      />
      <div class="error-message" v-if="!v.clientForm.birthday.required">Это обязательное поле</div>
      <div
        class="error-message"
        v-if="v.clientForm.birthday.$error"
      >Должна быть прошедшей в формате дд.мм.гггг</div>
    </div>
        <div class="field">
      <label class="label" for="gender">Пол</label>
      <ul id="gender" class="vue-form-list">
        <li>
          <input type="radio" name="gender" v-model="clientForm.gender" id="male" value="male" />
          <label class="label" for="male">Мужской</label>
        </li>
        <li>
          <input type="radio" name="gender" v-model="clientForm.gender" id="female" value="female" />
          <label class="label" for="female">Женский</label>
        </li>
      </ul>
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
      required: true,
    },
    step:{
      type: Number,
      required: true,
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
      },
    },
  },
};
</script>

<style scoped>
</style>
