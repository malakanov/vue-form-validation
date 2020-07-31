<template>
  <form class="vue-form" @submit.prevent="someAction()">
    <div v-show="step === 1">
      <h2>Контакты</h2>
      <div class="field">
        <label for="lastName">Фамилия</label>
        <input
          id="lastName"
          placeholder="Введите фамилию"
          type="text"
          v-model.trim="lastName"
          @blur="$v.lastName.$touch()"
          :class="{ 'error': !$v.lastName.$error }"
        />
        <div class="error-message" v-if="!$v.lastName.required">Это обязательное поле</div>
        <div class="error-message" v-if="$v.lastName.$error">
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
          :class="{ 'error': $v.firstName.$error || !$v.firstName.required }"
        />
        <div class="error-message" v-if="!$v.firstName.required">Это обязательное поле</div>
        <div class="error-message" v-if="$v.firstName.$error">
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
          :class="{ 'error': $v.middleName.$error }"
        />
        <div class="error-message" v-if="$v.middleName.$error">
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
        <input 
        id="birthday" 
        type="date" 
        v-model="birthday" 
        @blur="$v.birthdayObj.$touch()" 
        :class="{ 'error': $v.birthdayObj.$error || !$v.birthdayObj.required }"
        />
        <div class="error-message" v-if="!$v.birthdayObj.required">Это обязательное поле</div>
        <div
          class="error-message"
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
          :class="{ 'error': $v.phone.$error }"
        />
        <div class="error-message" v-if="$v.phone.$error">Номер должен быть в формате 79127745157</div>
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
          <select multiple="true" v-model="multipleSelections" :class="{ 'error': !$v.multipleSelections.required}">
            <option v-for="asset in assets" :value="asset" :key="asset">{{asset}}</option>
          </select>
          
          <div class="error-message" v-if="!$v.multipleSelections.required">Это обязательное поле</div>
          
          <span>Вы выбрали группы: {{ multipleSelections }}</span>
        </span>
      </div>
      <div class="field">
        <label for="doctor">Лечащий врач</label>
        <select id="doctor" v-model="doctor">
          <option value="id0">Иванов</option>
          <option value="id1">Захаров</option>
          <option value="id2">Чернышева</option>
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
      <button @click.prevent="next()">Next</button>
    </div>

    <div v-show="step === 2">
      <h2>Адрес</h2>
      <div class="field">
        <label for="adress_index">Индекс</label>
        <input
          id="adress_index"
          placeholder="Введите индекс"
          type="text"
          v-model.trim="adressIndex"
          @blur="$v.adressIndex.$touch()"
          :class="{ 'error': $v.adressIndex.$error }"
        />
        <div class="error-message" v-if="$v.adressIndex.$error">Индекс должен быть в формате 455000</div>
      </div>
      <div class="field">
        <label for="adress_country">Страна</label>
        <input
          id="adress_country"
          placeholder="Введите название страны"
          type="text"
          v-model.trim="adressCountry"
          @blur="$v.adressCountry.$touch()"
          :class="{ 'error': $v.adressCountry.$error }"
        />

        <div class="error-message" v-if="$v.adressCountry.$error">
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
          :class="{ 'error': $v.adressRegion.$error }"
        />

        <div class="error-message" v-if="$v.adressRegion.$error">
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
          :class="{ 'error': $v.adressCity.$error || !$v.adressCity.required}"
        />
        <div class="error-message" v-if="!$v.adressCity.required">Это обязательное поле</div>

        <div class="error-message" v-if="$v.adressCity.$error">
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
          :class="{ 'error': $v.adressStreet.$error }"
        />

        <div class="error-message" v-if="$v.adressStreet.$error">
          <template
            v-if="!$v.adressStreet.maxLength"
          >Название улицы не должно превышать {{ $v.adressStreet.$params.maxLength.max }} символов</template>
          <template
            v-else-if="!$v.adressStreet.alphaNum"
          >Название улицы должно содержать только цифры и буквы в кириллице</template>
        </div>
      </div>
      <div class="field">
        <label for="adress_building">Дом</label>
        <input
          id="adress_building"
          placeholder="Введите номер дома"
          type="text"
          v-model.trim="adressBuilding"
          @blur="$v.adressBuilding.$touch()"
          :class="{ 'error': $v.adressBuilding.$error }"
        />
        <div
          class="error-message"
          v-if="$v.adressBuilding.$error"
        >Номер дома должен быть числом, числом с литерой или числом с дробью числа</div>
      </div>
      <button @click.prevent="prev()">Previous</button>
      <button @click.prevent="next()">Next</button>
    </div>

    <div v-show="step === 3">
      <h2>Документ</h2>
      <div class="field">
        <label for="documents">Выберите документ</label>
        <select id="documents" v-model="documents">
          <option value="documentsPassport">Паспорт</option>
          <option value="documentsBirth">Свид. о рождении</option>
          <option value="documentsDriver">Вод. удостоверение</option>
        </select>
      </div>
      <h2 v-if="documents == 'documentsPassport'">Паспорт</h2>
      <h2 v-else-if="documents == 'documentsBirth'">Свид. о рождении</h2>
      <h2 v-else-if="documents == 'documentsDriver'">Вод. удостоверение</h2>
      <template v-if="documents == 'documentsPassport'">
        <div class="field">
          <label for="passport_serial">Серия паспорта</label>
          <input
            id="passport_serial"
            placeholder="Введите серию паспорта"
            type="text"
            min="0"
            max="9999"
            v-model="passportSerial"
            @blur="$v.passportSerial.$touch()"
            :class="{ 'error': $v.passportSerial.$error }"
            :maxlength="$v.passportSerial.$params.maxLength.max"
          />
        
          <div
            class="error-message"
            v-if="$v.passportSerial.$error"
          >Серия паспорта должна быть числом из 4 знаков</div>
        </div>

        <div class="field">
          <label for="passport_number">Номер паспорта</label>
          <input
            id="passport_number"
            placeholder="Введите номер паспорта"
            type="text"
            min="0"
            max="999999"
            v-model="passportNumber"
            @blur="$v.passportNumber.$touch()"
            :class="{ 'error': $v.passportNumber.$error }"
            :maxlength="$v.passportNumber.$params.maxLength.max"
          />
          <div
            class="error-message"
            v-if="$v.passportNumber.$error"
           >Номер паспорта должен быть числом из 6 знаков</div>
        </div>

        <div class="field">
          <label for="passport_issued">Выдан</label>
          <textarea
            id="passport_issued"
            placeholder="Введите кем был выдан паспорт, не более 100 символов"
            v-model="$v.passportIssued.$model"
            @blur="$v.passportIssued.$touch()"
            :maxlength="$v.passportIssued.$params.maxLength.max"
            :minlength="$v.passportIssued.$params.minLength.min"
          />
          <span
            class="counter"
          >{{ passportIssued.length }} / {{ $v.passportIssued.$params.maxLength.max}}</span>
          <div class="error-message" v-if="$v.passportIssued.$error">Длина строки не менее 30 и не более 100 символов</div>
        </div>

        <div class="field">
          <label for="passport_date">Дата выдачи паспорта</label>
          <input
            id="passport_date"
            type="date"
            v-model="passportDate"
            @blur="$v.passportDateObj.$touch()"
            :class="{ 'error': !$v.passportDateObj.$error }"
          />
          <div class="error-message" v-if="!$v.passportDateObj.required">Это обязательное поле</div>
          <div
            class="error-message"
            v-if="$v.passportDateObj.$error"
          >Дата выдачи паспорта должна быть прошедшей в формате дд.мм.гггг</div>
        </div>
      </template>
      <button @click.prevent="prev()">Previous</button>
      <button type="submit" :disabled="$v.$invalid">Отправить форму</button>
    </div>
  </form>
</template>

<script>
import {
  required,
  maxLength,
  minLength,
  maxValue,
  minValue,
  numeric
} from "vuelidate/lib/validators";

export default {
  data() {
    return {
      step: 1,
      firstName: null,
      lastName: null,
      middleName: null,
      birthday: null,
      phone: null,
      gender: null,
      multipleSelections: [],
      assets: ["VIP", "Проблемные", "ОМС"],
      doctor: null,
      sms: null,
      adressIndex: null,
      adressCountry: null,
      adressRegion: null,
      adressCity: null,
      adressStreet: null,
      adressBuilding: null,
      documents: "documentsPassport",
      passportSerial: null,
      passportNumber: null,
      passportDate: null,
      passportIssued: ""
    };
  },
  computed: {
    passportDateObj() {
      return this.passportDate ? new Date(this.passportDate) : null;
    },
    birthdayObj() {
      return this.birthday ? new Date(this.birthday) : null;
    }
  },

  validations: {
    passportDateObj: {
      required,
      maxValue: maxValue(new Date()),
      minValue: minValue(new Date(1974, 8, 28))
    },
    birthdayObj: {
      required,
      maxValue: maxValue(new Date()),
      minValue: minValue(new Date(1920, 1, 1))
    },
    firstName: {
      required,
      maxLength: maxLength(30),
      alpha: val => /^[а-яё]*$/i.test(val)
    },
    lastName: {
      required,
      maxLength: maxLength(30),
      alpha: val => /^[а-яё]*$/i.test(val)
    },
    middleName: {
      maxLength: maxLength(30),
      alpha: val => /^[а-яё]*$/i.test(val)
    },
    phone: {
      maxLength: maxLength(12),
      mixLength: minLength(11),
      validFormat: val =>
        /^((7) ?)?((\(\d{3}\))|(\d{3}))?(\d{3}?\d{2}?\d{2})$/.test(val)
    },
    multipleSelections: {
      required
    },
    adressIndex: {
      validFormat: val => /^\d{6}$/.test(val)
    },
    adressCountry: {
      maxLength: maxLength(35),
      alpha: val =>
        /^[А-Я]{1}[А-Яа-я]{2}([-А-Яа-я]{0,2})?([-А-Яа-я’]{0,1})?([-А-Яа-яё]{0,2})?([А-Яа-я]{0,1})?([а-я]{0,12})?( [(А-Яа-я–]{1})?([А-Яа-я]{0,1})?([а-я]{0,8})?( [А-Я]{1})?([а-я]{4})?([)а-я]{0,1})?([а-я]{0,9})?( [А-Я]{1})?([а-я]{5,9})?$/i.test(
          val
        )
    },
    adressRegion: {
      maxLength: maxLength(50),
      alpha: val => /^[а-яё]*$/i.test(val)
    },
    adressCity: {
      required,
      maxLength: maxLength(35),
      alpha: val => /^[а-яё]+((?:[- ][а-яё]+)*)+$/i.test(val)
    },
    adressStreet: {
      maxLength: maxLength(50),
      alphaNum: val =>
        /^[0-9А-Я]{1}([0-9А-Яа-я]{0,1})?([А-Яа-я]{0,1})?([а-я]{0,14})?( [0-9А-Яа-я]{1,2})?([-А-Яа-я]{0,1})?([а-я]{0,4})?([-а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,2})?([-а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,1})?( [0-9А-Яа-я]{1})?([А-Яа-я]{0,3})?([а-я]{0,6})?([-а-я]{0,1})?([-0-9а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,2})?( [(0-9А-Яа-я]{1})?([0-9а-я]{1})?([А-Яа-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,3})?([)а-я]{0,1})?( [0-9А-Яа-я]{1})?([0-9а-я]{0,1})?(.{0,1})?([0-9а-я]{0,2})?([а-я]{0,3})?$/i.test(
          val
        )
    },
    adressBuilding: {
      validFormat: val => /^[1-9]\d*(?: ?(?:[А-Яа-я]|[/-] ?\d?))?$/.test(val)
    },
    passportSerial: {
      numeric,
      maxLength: maxLength(4),
      minLength: minLength(4),
      maxValue: maxValue(9999),
      minValue: minValue(0)
    },
    passportNumber: {
      numeric,
      maxLength: maxLength(6),
      minLength: minLength(6),
      maxValue: maxValue(999999),
      minValue: minValue(0)
    },
    passportIssued: {
      maxLength: maxLength(100),
      minLength: minLength(30)
    }
  },

  methods: {
    someAction() {
      alert("Форма отправлена");
    },
    prev() {
      this.step--;
    },
    next() {
      this.step++;
    }
  }
};
</script>

<style scoped>
/*.field {*/
/*  margin-bottom: 24px;*/
/*}*/

/*.field > label {*/
/*  margin-right: 8px;*/
/*}*/

/*input {*/
/*  border: 1px solid silver;*/
/*  border-radius: 4px;*/
/*  background: white;*/
/*  padding: 5px 10px;*/
/*}*/

/*.error {*/
/*  color: red;*/
/*  border-color: red;*/
/*}*/

/*.error:focus {*/
/*  outline-color: #f99;*/
/*}*/

/*.valid {*/
/*  border-color: #5a5;*/
/*  background: #efe;*/
/*}*/

/*.valid:focus {*/
/*  outline-color: #8e8;*/
/*}*/

*,
*::after,
*::before {
  box-sizing: border-box;
}

body {
  color: #fff;
  background: #949c4e;
  background: linear-gradient(
    115deg,
    rgba(86, 216, 228, 1) 10%,
    rgba(159, 1, 234, 1) 90%
  );
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", Helvetica, Arial,
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

html,
body,
.container {
  min-height: 100vh;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

a {
  color: #2c3e50;
  text-decoration: none;
}

header {
  position: relative;
  height: 150px;
  padding-top: 100px;
}

header h1 {
  text-align: center;
  font-size: 2.4rem;
  font-weight: 300;
}

#app {
  display: flex;
}

.vue-form {
  font-size: 16px;
  width: 500px;
  padding: 15px 30px;
  border-radius: 4px;
  margin: 50px auto;
  width: 500px;
  background-color: #fff;
  box-shadow: 0 4px 6px 0 rgba(0, 0, 0, 0.3);
}
.vue-form fieldset {
  margin: 24px 0 0 0;
}
.vue-form legend {
  padding-bottom: 10px;
  border-bottom: 1px solid #ecf0f1;
}
.vue-form div {
  position: relative;
  margin: 20px 0;
}
.vue-form h4,
.vue-form .label {
  color: #94aab0;
  margin-bottom: 10px;
}
.vue-form .label {
  display: block;
}
.vue-form input,
.vue-form textarea,
.vue-form select,
.vue-form label {
  color: #2b3e51;
}
.vue-form input[type="text"],
.vue-form input[type="number"],
.vue-form input[type="email"],
.vue-form textarea,
.vue-form select,
.vue-form legend {
  display: block;
  width: 100%;
  appearance: none;
}
.vue-form input[type="text"],
.vue-form input[type="number"],
.vue-form input[type="email"],
.vue-form textarea,
.vue-form select {
  padding: 12px;
  border: 1px solid #cfd9db;
  background-color: #ffffff;
  border-radius: 0.25em;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.08);
}
.vue-form input[type="text"]:focus,
.vue-form input[type="number"]:focus,
.vue-form input[type="email"]:focus,
.vue-form textarea:focus,
.vue-form select:focus {
  outline: none;
  border-color: #2c3e50;
  box-shadow: 0 0 5px rgba(44, 151, 222, 0.2);
}
.vue-form .select {
  position: relative;
}
.vue-form .select::after {
  content: "";
  position: absolute;
  z-index: 1;
  right: 16px;
  top: 50%;
  margin-top: -8px;
  display: block;
  width: 16px;
  height: 16px;
  background: url("data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Cg%3E%0D%0A%09%3Cpolygon%20fill%3D%22%232c3e50%22%20points%3D%220.9%2C5.5%203.1%2C3.4%208%2C8.3%2012.9%2C3.4%2015.1%2C5.5%208%2C12.6%20%09%22%2F%3E%0D%0A%3C%2Fg%3E%0D%0A%3C%2Fsvg%3E")
    no-repeat center center;
  pointer-events: none;
}
.vue-form select {
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
  cursor: pointer;
}
.vue-form select::-ms-expand {
  display: none;
}
.vue-form .vue-form-list {
  margin-top: 16px;
}
.vue-form .vue-form-list::after {
  clear: both;
  content: "";
  display: table;
}
.vue-form .vue-form-list li {
  display: inline-block;
  position: relative;
  user-select: none;
  margin: 0 26px 16px 0;
}
.vue-form input[type="radio"],
.vue-form input[type="checkbox"] {
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  margin: 0;
  padding: 0;
  opacity: 0;
  z-index: 2;
}
.vue-form input[type="radio"] + label,
.vue-form input[type="checkbox"] + label {
  padding-left: 24px;
}
.vue-form input[type="radio"] + label::before,
.vue-form input[type="radio"] + label::after,
.vue-form input[type="checkbox"] + label::before,
.vue-form input[type="checkbox"] + label::after {
  content: "";
  display: block;
  position: absolute;
  left: 0;
  top: 50%;
  margin-top: -8px;
  width: 16px;
  height: 16px;
}
.vue-form input[type="radio"] + label::before,
.vue-form input[type="checkbox"] + label::before {
  border: 1px solid #cfd9db;
  background: #ffffff;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.08);
}
.vue-form input[type="radio"] + label::before,
.vue-form input[type="radio"] + label::after {
  border-radius: 50%;
}
.vue-form input[type="checkbox"] + label::before,
.vue-form input[type="checkbox"] + label::after {
  border-radius: 0.25em;
}
.vue-form input[type="radio"] + label::after,
.vue-form input[type="checkbox"] + label::after {
  background-color: #2c3e50;
  background-position: center center;
  background-repeat: no-repeat;
  box-shadow: 0 0 5px rgba(44, 151, 222, 0.4);
  display: none;
}
.vue-form input[type="radio"] + label::after {
  background-image: url("data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Ccircle%20fill%3D%22%23FFFFFF%22%20cx%3D%228%22%20cy%3D%228%22%20r%3D%223%22%2F%3E%0D%0A%3C%2Fsvg%3E");
}
.vue-form input[type="checkbox"] + label::after {
  background-image: url("data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21--%20Generator%3A%20Adobe%20Illustrator%2018.1.1%2C%20SVG%20Export%20Plug-In%20.%20SVG%20Version%3A%206.00%20Build%200%29%20%20--%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Cpolyline%20fill%3D%22none%22%20stroke%3D%22%23FFFFFF%22%20stroke-width%3D%222%22%20stroke-linecap%3D%22square%22%20stroke-miterlimit%3D%2210%22%20points%3D%225%2C8%207%2C10%2011%2C6%20%22%2F%3E%0D%0A%3C%2Fsvg%3E");
}
.vue-form input[type="radio"]:focus + label::before,
.vue-form input[type="checkbox"]:focus + label::before {
  box-shadow: 0 0 5px rgba(44, 151, 222, 0.6);
}
.vue-form input[type="radio"]:checked + label::after,
.vue-form input[type="checkbox"]:checked + label::after {
  display: block;
}
.vue-form input[type="radio"]:checked + label::before,
.vue-form input[type="radio"]:checked + label::after,
.vue-form input[type="checkbox"]:checked + label::before,
.vue-form input[type="checkbox"]:checked + label::after {
  animation: cd-bounce 0.3s;
}
.vue-form textarea {
  min-height: 120px;
  resize: vertical;
  overflow: auto;
}
.vue-form input[type="submit"] {
  border: none;
  background: #2c3e50;
  border-radius: 0.25em;
  padding: 12px 20px;
  color: #ffffff;
  font-weight: bold;
  float: right;
  cursor: pointer;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  appearance: none;
}
.no-touch .vue-form input[type="submit"]:hover {
  background: #42a2e1;
}
.vue-form input[type="submit"]:focus {
  outline: none;
  background: #2b3e51;
}
.vue-form input[type="submit"]:active {
  transform: scale(0.9);
}
.vue-form .error-message {
  margin: 5px;
  font-size: 14px;
  color: red;
}
.vue-form .error-message p {
  background: #e94b35;
  color: #ffffff;
  font-size: 1.4rem;
  text-align: center;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border-radius: 0.25em;
  padding: 16px;
}
.vue-form .error {
  border-color: red !important;
}
.vue-form .counter {
  background-color: #ecf0f1;
  position: absolute;
  right: 0px;
  top: 0px;
  font-size: 10px;
  padding: 4px;
}

.debug {
  border-radius: 4px;
  margin: 50px auto;
  width: 500px;
  background-color: #000;
  padding: 50px;
  background: rgba(0, 0, 0, 0.8);
  box-shadow: 0 4px 6px 0 rgba(0, 0, 0, 0.3);
}

.debug pre {
  color: #ffffff;
  font-size: 18px;
  line-height: 30px;
  font-family: "Source Code Pro", monospace;
  font-weight: 300;
  white-space: pre-wrap;
}

@-webkit-keyframes cd-bounce {
  0%,
  100% {
    -webkit-transform: scale(1);
  }
  50% {
    -webkit-transform: scale(0.8);
  }
}
@-moz-keyframes cd-bounce {
  0%,
  100% {
    -moz-transform: scale(1);
  }
  50% {
    -moz-transform: scale(0.8);
  }
}
@keyframes cd-bounce {
  0%,
  100% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.8);
  }
}
</style>
