<template>
  <div>
    <div class="field">
      <label class="label" for="phone">Номер телефона</label>
      <input
        id="phone"
        placeholder="79127745157"
        type="tel"
        v-model.trim="contactsForm.phone"
        @blur="v.contactsForm.phone.$touch()"
        :class="{ 'error': v.contactsForm.phone.$error || !v.contactsForm.phone.required }"
      />
      <div class="error-message" v-if="!v.contactsForm.phone.required">Это обязательное поле</div>
      <div
        class="error-message"
        v-if="v.contactsForm.phone.$error"
      >Номер должен быть в формате 79127745157</div>
    </div>

    <div class="field">
      <label class="label" for="groupClients">Группа клиентов</label>
      <span id="groupClients">
        <select
          multiple="true"
          v-model="contactsForm.multipleSelections"
          :class="{ 'error': !v.contactsForm.multipleSelections.required}"
        >
          <option v-for="asset in contactsForm.assets" :value="asset" :key="asset">{{asset}}</option>
        </select>

        <div
          class="error-message"
          v-if="!v.contactsForm.multipleSelections.required"
        >Это обязательное поле</div>

        
      </span>
      <ul v-for="multipleSelections in contactsForm.multipleSelections" :key="multipleSelections">
        <li>{{ multipleSelections }}</li>
      </ul>
    </div>
    <div class="field">
      <label class="label" for="doctor">Лечащий врач</label>
      <p class="select">
        <select class="budget" id="doctor" v-model="contactsForm.doctor">
          <option value="id0">Иванов</option>
          <option value="id1">Захаров</option>
          <option value="id2">Чернышева</option>
        </select>
      </p>
    </div>
    <div class="field">
      <label class="label" for="sms">Не отправлять СМС</label>
      <ul id="sms" class="vue-form-list">
        <li>
          <input type="radio" name="sms" v-model="contactsForm.sms" id="yesSms" value="1" />
          <label class="label" for="yesSms">Да</label>
        </li>
        <li>
          <input type="radio" name="sms" v-model="contactsForm.sms" id="noSms" value="0" />
          <label class="label" for="noSms">Нет</label>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContactsComponent",
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
    contactsForm: {
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
