<!--<template>-->
<!--  <form class="vue-form" @submit.prevent="someAction()">-->
<!--    <div v-show="step === 1">-->
<!--      <h2>Контакты</h2>-->
<!--      <div class="field">-->
<!--        <label for="lastName">Фамилия</label>-->
<!--        <input-->
<!--          id="lastName"-->
<!--          placeholder="Введите фамилию"-->
<!--          type="text"-->
<!--          v-model.trim="lastName"-->
<!--          @blur="$v.lastName.$touch()"-->
<!--          :class="{ 'error': !$v.lastName.$error }"-->
<!--        />-->
<!--        <div class="error-message" v-if="!$v.lastName.required">Это обязательное поле</div>-->
<!--        <div class="error-message" v-if="$v.lastName.$error">-->
<!--          <template-->
<!--            v-if="!$v.lastName.maxLength"-->
<!--          >Длина фамилии не должна превышать {{ $v.lastName.$params.maxLength.max }} символов</template>-->
<!--          <template v-else-if="!$v.lastName.alpha">Фамилия должна содержать только буквы в кириллице</template>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="firstName">Имя</label>-->
<!--        <input-->
<!--          id="firstName"-->
<!--          placeholder="Введите имя"-->
<!--          type="text"-->
<!--          v-model.trim="firstName"-->
<!--          @blur="$v.firstName.$touch()"-->
<!--          :class="{ 'error': $v.firstName.$error || !$v.firstName.required }"-->
<!--        />-->
<!--        <div class="error-message" v-if="!$v.firstName.required">Это обязательное поле</div>-->
<!--        <div class="error-message" v-if="$v.firstName.$error">-->
<!--          <template-->
<!--            v-if="!$v.firstName.maxLength"-->
<!--          >Длина имени не должна превышать {{ $v.firstName.$params.maxLength.max }} символов</template>-->
<!--          <template v-else-if="!$v.firstName.alpha">Имя должно содержать только буквы в кириллице</template>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="middleName">Отчество</label>-->
<!--        <input-->
<!--          id="middleName"-->
<!--          placeholder="Введите отчество"-->
<!--          type="text"-->
<!--          v-model.trim="middleName"-->
<!--          @blur="$v.middleName.$touch()"-->
<!--          :class="{ 'error': $v.middleName.$error }"-->
<!--        />-->
<!--        <div class="error-message" v-if="$v.middleName.$error">-->
<!--          <template-->
<!--            v-if="!$v.middleName.maxLength"-->
<!--          >Длина отчества не должна превышать {{ $v.middleName.$params.maxLength.max }} символов</template>-->
<!--          <template-->
<!--            v-else-if="!$v.middleName.alpha"-->
<!--          >Отчество должно содержать только буквы в кириллице</template>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="birthday">Дата рождения</label>-->
<!--        <input-->
<!--        id="birthday"-->
<!--        type="date"-->
<!--        v-model="birthday"-->
<!--        @blur="$v.birthdayObj.$touch()"-->
<!--        :class="{ 'error': $v.birthdayObj.$error || !$v.birthdayObj.required }"-->
<!--        />-->
<!--        <div class="error-message" v-if="!$v.birthdayObj.required">Это обязательное поле</div>-->
<!--        <div-->
<!--          class="error-message"-->
<!--          v-if="$v.birthdayObj.$error"-->
<!--        >Дата рождения должна быть прошедшей в формате дд.мм.гггг</div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="phone">Номер телефона</label>-->
<!--        <input-->
<!--          id="phone"-->
<!--          placeholder="79127745157"-->
<!--          type="tel"-->
<!--          v-model.trim="phone"-->
<!--          @blur="$v.phone.$touch()"-->
<!--          :class="{ 'error': $v.phone.$error }"-->
<!--        />-->
<!--        <div class="error-message" v-if="$v.phone.$error">Номер должен быть в формате 79127745157</div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="gender">Пол</label>-->
<!--        <span id="gender">-->
<!--          <input type="radio" name="gender" v-model="gender" id="gender1" value="male" />-->
<!--          <label for="gender1">Мужской</label>-->
<!--          <input type="radio" name="gender" v-model="gender" id="gender2" value="female" />-->
<!--          <label for="gender2">Женский</label>-->
<!--        </span>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="groupClients">Группа клиентов</label>-->
<!--        <span id="groupClients">-->
<!--          <select multiple="true" v-model="multipleSelections" :class="{ 'error': !$v.multipleSelections.required}">-->
<!--            <option v-for="asset in assets" :value="asset" :key="asset">{{asset}}</option>-->
<!--          </select>-->

<!--          <div class="error-message" v-if="!$v.multipleSelections.required">Это обязательное поле</div>-->

<!--          <span>Вы выбрали группы: {{ multipleSelections }}</span>-->
<!--        </span>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="doctor">Лечащий врач</label>-->
<!--        <select id="doctor" v-model="doctor">-->
<!--          <option value="id0">Иванов</option>-->
<!--          <option value="id1">Захаров</option>-->
<!--          <option value="id2">Чернышева</option>-->
<!--        </select>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="sms">Не отправлять СМС</label>-->
<!--        <span id="sms">-->
<!--          <input type="radio" name="sms" v-model="sms" id="yesSms" value="1" />-->
<!--          <label for="yesSms">Да</label>-->
<!--          <input type="radio" name="sms" v-model="sms" id="noSms" value="0" />-->
<!--          <label for="noSms">Нет</label>-->
<!--        </span>-->
<!--      </div>-->
<!--      <button @click.prevent="next()">Next</button>-->
<!--    </div>-->

<!--    <div v-show="step === 2">-->
<!--      <h2>Адрес</h2>-->
<!--      <div class="field">-->
<!--        <label for="adress_index">Индекс</label>-->
<!--        <input-->
<!--          id="adress_index"-->
<!--          placeholder="Введите индекс"-->
<!--          type="text"-->
<!--          v-model.trim="adressIndex"-->
<!--          @blur="$v.adressIndex.$touch()"-->
<!--          :class="{ 'error': $v.adressIndex.$error }"-->
<!--        />-->
<!--        <div class="error-message" v-if="$v.adressIndex.$error">Индекс должен быть в формате 455000</div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="adress_country">Страна</label>-->
<!--        <input-->
<!--          id="adress_country"-->
<!--          placeholder="Введите название страны"-->
<!--          type="text"-->
<!--          v-model.trim="adressCountry"-->
<!--          @blur="$v.adressCountry.$touch()"-->
<!--          :class="{ 'error': $v.adressCountry.$error }"-->
<!--        />-->

<!--        <div class="error-message" v-if="$v.adressCountry.$error">-->
<!--          <template-->
<!--            v-if="!$v.adressCountry.maxLength"-->
<!--          >Название страны не должно превышать {{ $v.adressCountry.$params.maxLength.max }} символов</template>-->
<!--          <template-->
<!--            v-else-if="!$v.adressCountry.alpha"-->
<!--          >Название страны должно содержать только буквы в кириллице</template>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="adress_region">Область</label>-->
<!--        <input-->
<!--          id="adress_region"-->
<!--          placeholder="Введите название области"-->
<!--          type="text"-->
<!--          v-model.trim="adressRegion"-->
<!--          @blur="$v.adressRegion.$touch()"-->
<!--          :class="{ 'error': $v.adressRegion.$error }"-->
<!--        />-->

<!--        <div class="error-message" v-if="$v.adressRegion.$error">-->
<!--          <template-->
<!--            v-if="!$v.adressRegion.maxLength"-->
<!--          >Название области не должно превышать {{ $v.adressRegion.$params.maxLength.max }} символов</template>-->
<!--          <template-->
<!--            v-else-if="!$v.adressRegion.alpha"-->
<!--          >Название области должно содержать только буквы в кириллице</template>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="adress_city">Город</label>-->
<!--        <input-->
<!--          id="adress_city"-->
<!--          placeholder="Введите название города"-->
<!--          type="text"-->
<!--          v-model.trim="adressCity"-->
<!--          @blur="$v.adressCity.$touch()"-->
<!--          :class="{ 'error': $v.adressCity.$error || !$v.adressCity.required}"-->
<!--        />-->
<!--        <div class="error-message" v-if="!$v.adressCity.required">Это обязательное поле</div>-->

<!--        <div class="error-message" v-if="$v.adressCity.$error">-->
<!--          <template-->
<!--            v-if="!$v.adressCity.maxLength"-->
<!--          >Название города не должно превышать {{ $v.adressCity.$params.maxLength.max }} символов</template>-->
<!--          <template-->
<!--            v-else-if="!$v.adressCity.alpha"-->
<!--          >Название города должно содержать только буквы в кириллице</template>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="adress_street">Улица</label>-->
<!--        <input-->
<!--          id="adress_street"-->
<!--          placeholder="Введите название улицы"-->
<!--          type="text"-->
<!--          v-model.trim="adressStreet"-->
<!--          @blur="$v.adressStreet.$touch()"-->
<!--          :class="{ 'error': $v.adressStreet.$error }"-->
<!--        />-->

<!--        <div class="error-message" v-if="$v.adressStreet.$error">-->
<!--          <template-->
<!--            v-if="!$v.adressStreet.maxLength"-->
<!--          >Название улицы не должно превышать {{ $v.adressStreet.$params.maxLength.max }} символов</template>-->
<!--          <template-->
<!--            v-else-if="!$v.adressStreet.alphaNum"-->
<!--          >Название улицы должно содержать только цифры и буквы в кириллице</template>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="field">-->
<!--        <label for="adress_building">Дом</label>-->
<!--        <input-->
<!--          id="adress_building"-->
<!--          placeholder="Введите номер дома"-->
<!--          type="text"-->
<!--          v-model.trim="adressBuilding"-->
<!--          @blur="$v.adressBuilding.$touch()"-->
<!--          :class="{ 'error': $v.adressBuilding.$error }"-->
<!--        />-->
<!--        <div-->
<!--          class="error-message"-->
<!--          v-if="$v.adressBuilding.$error"-->
<!--        >Номер дома должен быть числом, числом с литерой или числом с дробью числа</div>-->
<!--      </div>-->
<!--      <button @click.prevent="prev()">Previous</button>-->
<!--      <button @click.prevent="next()">Next</button>-->
<!--    </div>-->

<!--    <div v-show="step === 3">-->
<!--      <h2>Документ</h2>-->
<!--      <div class="field">-->
<!--        <label for="documents">Выберите документ</label>-->
<!--        <select id="documents" v-model="documents">-->
<!--          <option value="documentsPassport">Паспорт</option>-->
<!--          <option value="documentsBirth">Свид. о рождении</option>-->
<!--          <option value="documentsDriver">Вод. удостоверение</option>-->
<!--        </select>-->
<!--      </div>-->
<!--      <h2 v-if="documents == 'documentsPassport'">Паспорт</h2>-->
<!--      <h2 v-else-if="documents == 'documentsBirth'">Свид. о рождении</h2>-->
<!--      <h2 v-else-if="documents == 'documentsDriver'">Вод. удостоверение</h2>-->
<!--      <template v-if="documents == 'documentsPassport'">-->
<!--        <div class="field">-->
<!--          <label for="passport_serial">Серия паспорта</label>-->
<!--          <input-->
<!--            id="passport_serial"-->
<!--            placeholder="Введите серию паспорта"-->
<!--            type="text"-->
<!--            min="0"-->
<!--            max="9999"-->
<!--            v-model="passportSerial"-->
<!--            @blur="$v.passportSerial.$touch()"-->
<!--            :class="{ 'error': $v.passportSerial.$error }"-->
<!--            :maxlength="$v.passportSerial.$params.maxLength.max"-->
<!--          />-->

<!--          <div-->
<!--            class="error-message"-->
<!--            v-if="$v.passportSerial.$error"-->
<!--          >Серия паспорта должна быть числом из 4 знаков</div>-->
<!--        </div>-->

<!--        <div class="field">-->
<!--          <label for="passport_number">Номер паспорта</label>-->
<!--          <input-->
<!--            id="passport_number"-->
<!--            placeholder="Введите номер паспорта"-->
<!--            type="text"-->
<!--            min="0"-->
<!--            max="999999"-->
<!--            v-model="passportNumber"-->
<!--            @blur="$v.passportNumber.$touch()"-->
<!--            :class="{ 'error': $v.passportNumber.$error }"-->
<!--            :maxlength="$v.passportNumber.$params.maxLength.max"-->
<!--          />-->
<!--          <div-->
<!--            class="error-message"-->
<!--            v-if="$v.passportNumber.$error"-->
<!--           >Номер паспорта должен быть числом из 6 знаков</div>-->
<!--        </div>-->

<!--        <div class="field">-->
<!--          <label for="passport_issued">Выдан</label>-->
<!--          <textarea-->
<!--            id="passport_issued"-->
<!--            placeholder="Введите кем был выдан паспорт, не более 100 символов"-->
<!--            v-model="$v.passportIssued.$model"-->
<!--            @blur="$v.passportIssued.$touch()"-->
<!--            :maxlength="$v.passportIssued.$params.maxLength.max"-->
<!--            :minlength="$v.passportIssued.$params.minLength.min"-->
<!--          />-->
<!--          <span-->
<!--            class="counter"-->
<!--          >{{ passportIssued.length }} / {{ $v.passportIssued.$params.maxLength.max}}</span>-->
<!--          <div class="error-message" v-if="$v.passportIssued.$error">Длина строки не менее 30 и не более 100 символов</div>-->
<!--        </div>-->

<!--        <div class="field">-->
<!--          <label for="passport_date">Дата выдачи паспорта</label>-->
<!--          <input-->
<!--            id="passport_date"-->
<!--            type="date"-->
<!--            v-model="passportDate"-->
<!--            @blur="$v.passportDateObj.$touch()"-->
<!--            :class="{ 'error': !$v.passportDateObj.$error }"-->
<!--          />-->
<!--          <div class="error-message" v-if="!$v.passportDateObj.required">Это обязательное поле</div>-->
<!--          <div-->
<!--            class="error-message"-->
<!--            v-if="$v.passportDateObj.$error"-->
<!--          >Дата выдачи паспорта должна быть прошедшей в формате дд.мм.гггг</div>-->
<!--        </div>-->
<!--      </template>-->
<!--      <button @click.prevent="prev()">Previous</button>-->
<!--      <button type="submit" :disabled="$v.$invalid">Отправить форму</button>-->
<!--    </div>-->
<!--  </form>-->
<!--</template>-->

<!--<script>-->
<!--import {-->
<!--  required,-->
<!--  maxLength,-->
<!--  minLength,-->
<!--  maxValue,-->
<!--  minValue,-->
<!--  numeric-->
<!--} from "vuelidate/lib/validators";-->

<!--export default {-->
<!--  data() {-->
<!--    return {-->
<!--      step: 1,-->
<!--      firstName: null,-->
<!--      lastName: null,-->
<!--      middleName: null,-->
<!--      birthday: null,-->
<!--      phone: null,-->
<!--      gender: null,-->
<!--      multipleSelections: [],-->
<!--      assets: ["VIP", "Проблемные", "ОМС"],-->
<!--      doctor: null,-->
<!--      sms: null,-->
<!--      adressIndex: null,-->
<!--      adressCountry: null,-->
<!--      adressRegion: null,-->
<!--      adressCity: null,-->
<!--      adressStreet: null,-->
<!--      adressBuilding: null,-->
<!--      documents: "documentsPassport",-->
<!--      passportSerial: null,-->
<!--      passportNumber: null,-->
<!--      passportDate: null,-->
<!--      passportIssued: ""-->
<!--    };-->
<!--  },-->
<!--  computed: {-->
<!--    passportDateObj() {-->
<!--      return this.passportDate ? new Date(this.passportDate) : null;-->
<!--    },-->
<!--    birthdayObj() {-->
<!--      return this.birthday ? new Date(this.birthday) : null;-->
<!--    }-->
<!--  },-->

<!--  validations: {-->
<!--    passportDateObj: {-->
<!--      required,-->
<!--      maxValue: maxValue(new Date()),-->
<!--      minValue: minValue(new Date(1974, 8, 28))-->
<!--    },-->
<!--    birthdayObj: {-->
<!--      required,-->
<!--      maxValue: maxValue(new Date()),-->
<!--      minValue: minValue(new Date(1920, 1, 1))-->
<!--    },-->
<!--    firstName: {-->
<!--      required,-->
<!--      maxLength: maxLength(30),-->
<!--      alpha: val => /^[а-яё]*$/i.test(val)-->
<!--    },-->
<!--    lastName: {-->
<!--      required,-->
<!--      maxLength: maxLength(30),-->
<!--      alpha: val => /^[а-яё]*$/i.test(val)-->
<!--    },-->
<!--    middleName: {-->
<!--      maxLength: maxLength(30),-->
<!--      alpha: val => /^[а-яё]*$/i.test(val)-->
<!--    },-->
<!--    phone: {-->
<!--      maxLength: maxLength(12),-->
<!--      mixLength: minLength(11),-->
<!--      validFormat: val =>-->
<!--        /^((7) ?)?((\(\d{3}\))|(\d{3}))?(\d{3}?\d{2}?\d{2})$/.test(val)-->
<!--    },-->
<!--    multipleSelections: {-->
<!--      required-->
<!--    },-->
<!--    adressIndex: {-->
<!--      validFormat: val => /^\d{6}$/.test(val)-->
<!--    },-->
<!--    adressCountry: {-->
<!--      maxLength: maxLength(35),-->
<!--      alpha: val =>-->
<!--        /^[А-Я]{1}[А-Яа-я]{2}([-А-Яа-я]{0,2})?([-А-Яа-я’]{0,1})?([-А-Яа-яё]{0,2})?([А-Яа-я]{0,1})?([а-я]{0,12})?( [(А-Яа-я–]{1})?([А-Яа-я]{0,1})?([а-я]{0,8})?( [А-Я]{1})?([а-я]{4})?([)а-я]{0,1})?([а-я]{0,9})?( [А-Я]{1})?([а-я]{5,9})?$/i.test(-->
<!--          val-->
<!--        )-->
<!--    },-->
<!--    adressRegion: {-->
<!--      maxLength: maxLength(50),-->
<!--      alpha: val => /^[а-яё]*$/i.test(val)-->
<!--    },-->
<!--    adressCity: {-->
<!--      required,-->
<!--      maxLength: maxLength(35),-->
<!--      alpha: val => /^[а-яё]+((?:[- ][а-яё]+)*)+$/i.test(val)-->
<!--    },-->
<!--    adressStreet: {-->
<!--      maxLength: maxLength(50),-->
<!--      alphaNum: val =>-->
<!--        /^[0-9А-Я]{1}([0-9А-Яа-я]{0,1})?([А-Яа-я]{0,1})?([а-я]{0,14})?( [0-9А-Яа-я]{1,2})?([-А-Яа-я]{0,1})?([а-я]{0,4})?([-а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,2})?([-а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,1})?( [0-9А-Яа-я]{1})?([А-Яа-я]{0,3})?([а-я]{0,6})?([-а-я]{0,1})?([-0-9а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,2})?( [(0-9А-Яа-я]{1})?([0-9а-я]{1})?([А-Яа-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,3})?([)а-я]{0,1})?( [0-9А-Яа-я]{1})?([0-9а-я]{0,1})?(.{0,1})?([0-9а-я]{0,2})?([а-я]{0,3})?$/i.test(-->
<!--          val-->
<!--        )-->
<!--    },-->
<!--    adressBuilding: {-->
<!--      validFormat: val => /^[1-9]\d*(?: ?(?:[А-Яа-я]|[/-] ?\d?))?$/.test(val)-->
<!--    },-->
<!--    passportSerial: {-->
<!--      numeric,-->
<!--      maxLength: maxLength(4),-->
<!--      minLength: minLength(4),-->
<!--      maxValue: maxValue(9999),-->
<!--      minValue: minValue(0)-->
<!--    },-->
<!--    passportNumber: {-->
<!--      numeric,-->
<!--      maxLength: maxLength(6),-->
<!--      minLength: minLength(6),-->
<!--      maxValue: maxValue(999999),-->
<!--      minValue: minValue(0)-->
<!--    },-->
<!--    passportIssued: {-->
<!--      maxLength: maxLength(100),-->
<!--      minLength: minLength(30)-->
<!--    }-->
<!--  },-->

<!--  methods: {-->
<!--    someAction() {-->
<!--      alert("Форма отправлена");-->
<!--    },-->
<!--    prev() {-->
<!--      this.step&#45;&#45;;-->
<!--    },-->
<!--    next() {-->
<!--      this.step++;-->
<!--    }-->
<!--  }-->
<!--};-->
<!--</script>-->
<template>
  <div>
    
    <form-component />
  </div>

</template>

<script>
import FormComponent from "./components/FormComponent.vue";

export default {
  name: "App",
  components: {
    FormComponent
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


</style>
