<template>
  <form @submit.prevent="someAction()">
    <div class="field">
      <label for="lastName">Фамилия</label>
      <input
        id="lastName"
        placeholder="Введите фамилию"
        type="text"
        v-model.trim="lastName"
        @blur="$v.lastName.$touch()"
      />
      <span class="error" v-if="!$v.lastName.required">*</span>
      <div class="error" v-if="$v.lastName.$error">
        <template
          v-if="!$v.lastName.maxLength"
        >Длина фамилии не должна превышать {{ $v.lastName.$params.maxLength.max }} символов</template>
        <template v-else-if="!$v.lastName.alpha">Фамилия должна содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label for="firstName">Имя</label>
      <input
        id="firstName"
        placeholder="Введите имя"
        type="text"
        v-model.trim="firstName"
        @blur="$v.firstName.$touch()"
      />
      <span class="error" v-if="!$v.firstName.required">*</span>
      <div class="error" v-if="$v.firstName.$error">
        <template
          v-if="!$v.firstName.maxLength"
        >Длина имени не должна превышать {{ $v.firstName.$params.maxLength.max }} символов</template>
        <template v-else-if="!$v.firstName.alpha">Имя должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label for="middleName">Отчество</label>
      <input
        id="middleName"
        placeholder="Введите отчество"
        type="text"
        v-model.trim="middleName"
        @blur="$v.middleName.$touch()"
      />
      <div class="error" v-if="$v.middleName.$error">
        <template
          v-if="!$v.middleName.maxLength"
        >Длина отчества не должна превышать {{ $v.middleName.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!$v.middleName.alpha"
        >Отчество должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label for="birthday">Дата рождения</label>
      <input id="birthday" type="date" v-model="birthday" @blur="$v.birthdayObj.$touch()" />
      <span class="error" v-if="!$v.birthdayObj.required">*</span>
      <div
        class="error"
        v-if="$v.birthdayObj.$error"
      >Дата рождения должна быть прошедшей в формате дд.мм.гггг</div>
    </div>

    <div class="field">
      <label for="phone">Номер телефона</label>
      <input
        id="phone"
        placeholder="79127745157"
        type="tel"
        v-model.trim="phone"
        @blur="$v.phone.$touch()"
      />
      <div class="error" v-if="$v.phone.$error">Номер должен быть в формате 79127745157</div>
    </div>

    <div class="field">
      <label for="gender">Пол</label>
      <span id="gender">
        <input type="radio" name="gender" v-model="gender" id="gender1" value="male" />
        <label for="gender1">Мужской</label>
        <input type="radio" name="gender" v-model="gender" id="gender2" value="female" />
        <label for="gender2">Женский</label>
      </span>
    </div>

    <div class="field">
      <label for="groupClients">Группа клиентов</label>
      <span id="groupClients">
        <select multiple="true" v-model="multipleSelections">
          <option v-for="asset in assets" :value="asset" :key="asset">{{asset}}</option>
        </select>
        <span class="error" v-if="!$v.multipleSelections.required">*</span>
        <span>Вы выбрали группы: {{ multipleSelections }}</span>
      </span>
    </div>

    <div class="field">
      <label for="doctor">Лечащий врач</label>
      <select id="doctor" v-model="doctor">
        <option value>Иванов</option>
        <option value="alpha">Захаров</option>
        <option value="beta">Чернышева</option>
      </select>
    </div>

    <div class="field">
      <label for="sms">Не отправлять СМС</label>
      <span id="sms">
        <input type="radio" name="sms" v-model="sms" id="yesSms" value="1" />
        <label for="yesSms">Да</label>
        <input type="radio" name="sms" v-model="sms" id="noSms" value="0" />
        <label for="noSms">Нет</label>
      </span>
    </div>

    <h2>Адрес</h2>

    <div class="field">
      <label for="adress_index">Индекс</label>
      <input
        id="adress_index"
        placeholder="Введите индекс"
        type="text"
        v-model.trim="adressIndex"
        @blur="$v.adressIndex.$touch()"
      />
      <div class="error" v-if="$v.adressIndex.$error">Индекс должен быть в формате 455000</div>
    </div>

    <div class="field">
      <label for="adress_country">Страна</label>
      <input
        id="adress_country"
        placeholder="Введите название страны"
        type="text"
        v-model.trim="adressCountry"
        @blur="$v.adressCountry.$touch()"
      />

      <div class="error" v-if="$v.adressCountry.$error">
        <template
          v-if="!$v.adressCountry.maxLength"
        >Название страны не должно превышать {{ $v.adressCountry.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!$v.adressCountry.alpha"
        >Название страны должно содержать только буквы в кириллице</template>
      </div>
    </div>
    
    <div class="field">
      <label for="adress_region">Область</label>
      <input
        id="adress_region"
        placeholder="Введите название области"
        type="text"
        v-model.trim="adressRegion"
        @blur="$v.adressRegion.$touch()"
      />

      <div class="error" v-if="$v.adressRegion.$error">
        <template
          v-if="!$v.adressRegion.maxLength"
        >Название области не должно превышать {{ $v.adressRegion.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!$v.adressRegion.alpha"
        >Название области должно содержать только буквы в кириллице</template>
      </div>
    </div>
    
    <div class="field">
      <label for="adress_city">Город</label>
      <input
        id="adress_city"
        placeholder="Введите название города"
        type="text"
        v-model.trim="adressCity"
        @blur="$v.adressCity.$touch()"
      />
      <span class="error" v-if="!$v.adressCity.required">*</span>

      <div class="error" v-if="$v.adressCity.$error">
        <template
          v-if="!$v.adressCity.maxLength"
        >Название города не должно превышать {{ $v.adressCity.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!$v.adressCity.alpha"
        >Название города должно содержать только буквы в кириллице</template>
      </div>
    </div>
    
    <div class="field">
      <label for="adress_street">Улица</label>
      <input
        id="adress_street"
        placeholder="Введите название улицы"
        type="text"
        v-model.trim="adressStreet"
        @blur="$v.adressStreet.$touch()"
      />

      <div class="error" v-if="$v.adressStreet.$error">
        <template
          v-if="!$v.adressStreet.maxLength"
        >Название улицы не должно превышать {{ $v.adressStreet.$params.maxLength.max }} символов</template>
        <template
          v-else-if="!$v.adressStreet.alphaNum"
        >Название улицы должно содержать только цифры и буквы в кириллице</template>
      </div>
    </div>

    <div class="field">
      <label for="passport_data">Серия и номер паспорта</label>
      <input
        id="passport_data"
        placeholder="1234 567890"
        type="text"
        v-model.trim="passportData"
        @blur="$v.passportData.$touch()"
      />
      <div
        class="error"
        v-if="$v.passportData.$error"
      >Серия и номер паспорта должны быть в формате 1234 567890</div>
    </div>

    <div class="field">
      <label for="passport_date">Дата выдачи паспорта</label>
      <input
        id="passport_date"
        type="date"
        v-model="passportDate"
        @blur="$v.passportDateObj.$touch()"
      />
      <span class="error" v-if="!$v.passportDateObj.required">*</span>
      <div
        class="error"
        v-if="$v.passportDateObj.$error"
      >Дата выдачи паспорта должна быть прошедшей в формате дд.мм.гггг</div>
    </div>

    <button type="submit" :disabled="$v.$invalid">Отправить форму</button>
  </form>
</template>

<script>
import {
  required,
  maxLength,
  minLength,
  maxValue,
  minValue,
} from "vuelidate/lib/validators";

export default {
  data() {
    return {
      passportData: null,
      firstName: null,
      lastName: null,
      middleName: null,
      birthday: null,
      phone: null,
      gender: null,
      multipleSelections: null,
      assets: ["VIP", "Проблемные", "ОМС"],
      doctor: null,
      sms: null,
      adressIndex: null,
      adressCountry: null,
      adressRegion: null,
      adressCity: null,
      adressStreet: null,
      passportDate: null,
    };
  },
  computed: {
    passportDateObj() {
      return this.passportDate ? new Date(this.passportDate) : null;
    },
    birthdayObj() {
      return this.birthday ? new Date(this.birthday) : null;
    },
  },

  validations: {
    passportData: {
      required,
      validFormat: (val) => /^\d{4} \d{6}$/.test(val),
    },
    passportDateObj: {
      required,
      maxValue: maxValue(new Date()),
      minValue: minValue(new Date(1974, 8, 28)),
    },
    birthdayObj: {
      required,
      maxValue: maxValue(new Date()),
      minValue: minValue(new Date(1920, 1, 1)),
    },
    firstName: {
      required,
      maxLength: maxLength(30),
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    lastName: {
      required,
      maxLength: maxLength(30),
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    middleName: {
      maxLength: maxLength(30),
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    phone: {
      maxLength: maxLength(12),
      mixLength: minLength(11),
      validFormat: (val) =>
        /^((7) ?)?((\(\d{3}\))|(\d{3}))?(\d{3}?\d{2}?\d{2})$/.test(val),
    },
    multipleSelections: {
      required,
    },
    adressIndex: {
      validFormat: (val) => /^\d{6}$/.test(val),
    },
    adressCountry: {
      maxLength: maxLength(35),
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    adressRegion: {
      maxLength: maxLength(50),
      alpha: (val) => /^[а-яё]*$/i.test(val),
    },
    adressCity: {
      required,
      maxLength: maxLength(35),
      alpha: (val) => /^[а-яё]+((?:[- ][а-яё]+)*)+$/i.test(val),
    },
    adressStreet: {
      maxLength: maxLength(50),
      alphaNum: (val) => /^[A-Za-z0-9]+$/i.test(val),
    },
  },

  methods: {
    someAction() {
      alert("Форма отправлена");
    },
  },
};
</script>

<style scoped>
.field {
  margin-bottom: 24px;
}

.field > label {
  margin-right: 8px;
}

input {
  border: 1px solid silver;
  border-radius: 4px;
  background: white;
  padding: 5px 10px;
}

.error {
  color: red;
  border-color: red;
}

.error:focus {
  outline-color: #f99;
}

.valid {
  border-color: #5a5;
  background: #efe;
}

.valid:focus {
  outline-color: #8e8;
}
</style>
