<template>
  <div>
    {{ clientForm }}
    {{ v.clientForm.lastName }}
    <h2>Клиент</h2>
    <div class="field">
      <label for="lastName">Фамилия</label>
      <input
        id="lastName"
        placeholder="Введите фамилию"
        type="text"
        v-model.trim="clientForm.lastName"
        :class="{ 'error': !v.clientForm.lastName.$error }"
      />
      <div class="error-message" v-if="!v.clientForm.lastName.required">Это обязательное поле</div>
      <div class="error-message" v-if="!v.clientForm.lastName.$error">
        <template
          v-if="!v.clientForm.lastName.maxLength"
        >Длина фамилии не должна превышать {{ v.clientForm.lastName.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!v.clientForm.lastName.alpha"
        >Фамилия должна содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label for="firstName">Имя</label>
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
        >Имя должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label for="middleName">Отчество</label>
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
        >Отчество должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label for="birthday">Дата рождения</label>
      <input
        id="birthday"
        type="date"
        v-model="clientForm.birthday"
        @blur="v.clientForm.birthdayObj.$touch()"
        :class="{ 'error': v.clientForm.birthdayObj.$error || !v.clientForm.birthdayObj.required }"
      />
      <div class="error-message" v-if="!v.clientForm.birthdayObj.required">Это обязательное поле</div>
      <div
        class="error-message"
        v-if="v.clientForm.birthdayObj.$error"
      >Дата рождения должна быть прошедшей в формате дд.мм.гггг</div>
    </div>
    <div class="field">
      <label for="phone">Номер телефона</label>
      <input
        id="phone"
        placeholder="79127745157"
        type="tel"
        v-model.trim="clientForm.phone"
        @blur="v.clientForm.phone.$touch()"
        :class="{ 'error': v.clientForm.phone.$error }"
      />
      <div
        class="error-message"
        v-if="v.clientForm.phone.$error"
      >Номер должен быть в формате 79127745157</div>
    </div>
    <div class="field">
      <label for="gender">Пол</label>
      <span id="gender">
        <input type="radio" name="gender" v-model="clientForm.gender" id="male" value="male" />
        <label for="male">Мужской</label>
        <input type="radio" name="gender" v-model="clientForm.gender" id="female" value="female" />
        <label for="female">Женский</label>
      </span>
    </div>
    <div class="field">
      <label for="groupClients">Группа клиентов</label>
      <span id="groupClients">
        <select
          multiple="true"
          v-model="clientForm.multipleSelections"
          :class="{ 'error': !v.clientForm.multipleSelections.required}"
        >
          <option v-for="asset in clientForm.assets" :value="asset" :key="asset">{{asset}}</option>
        </select>

        <div
          class="error-message"
          v-if="!v.clientForm.multipleSelections.required"
        >Это обязательное поле</div>

        <span>Вы выбрали группы: {{ clientForm.multipleSelections }}</span>
      </span>
    </div>
    <div class="field">
      <label for="doctor">Лечащий врач</label>
      <select id="doctor" v-model="clientForm.doctor">
        <option value="id0">Иванов</option>
        <option value="id1">Захаров</option>
        <option value="id2">Чернышева</option>
      </select>
    </div>
    <div class="field">
      <label for="sms">Не отправлять СМС</label>
      <span id="sms">
        <input type="radio" name="sms" v-model="clientForm.sms" id="yesSms" value="1" />
        <label for="yesSms">Да</label>
        <input type="radio" name="sms" v-model="clientForm.sms" id="noSms" value="0" />
        <label for="noSms">Нет</label>
      </span>
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
