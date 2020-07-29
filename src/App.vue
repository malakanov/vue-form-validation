<template>
  <form @submit.prevent="someAction()">
    <div class="field">
      <label for="lastName">Фамилия</label>
      <input id="lastName" placeholder="Введите фамилию" type="text" v-model.trim="lastName" @blur="$v.lastName.$touch()" />
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
      <input id="firstName" placeholder="Введите имя" type="text" v-model.trim="firstName" @blur="$v.firstName.$touch()" />
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
      <input id="middleName" placeholder="Введите отчество" type="text" v-model.trim="middleName" @blur="$v.middleName.$touch()" />
      <div class="error" v-if="$v.middleName.$error">
        <template
            v-if="!$v.middleName.maxLength"
        >Длина отчества не должна превышать {{ $v.middleName.$params.maxLength.max }} символов</template>
        <template v-else-if="!$v.middleName.alpha">Отчество должно содержать только буквы в кириллице</template>
      </div>
    </div>
    <div class="field">
      <label for="birthday">Дата рождения</label>
      <input id="birthday" type="date" v-model="birthday" @blur="$v.birthdayObj.$touch()" />
      <span class="error" v-if="!$v.birthdayObj.required">*</span>
      <div
          class="error"
          v-if="$v.birthdayObj.$error"
      >Дата рождения должна быть прошедшей в формате дд.мм.гггг </div>
    </div>

    <div class="field">
      <label for="phone">Номер телефона</label>
      <input id="phone" placeholder="79127745157" type="tel" v-model.trim="phone" @blur="$v.phone.$touch()">
      <div
          class="error"
          v-if="$v.phone.$error"
      >Номер должен быть в формате 79127745157</div>
    </div>

    <div class="field">
        <label for="gender">Пол</label>
          <span id="gender">
            <input  type="radio" name="gender" v-model="gender" id="gender1" value="male" @blur="$v.gender.$touch()">
            <label  for="gender1">Мужской</label>
            <input type="radio" name="gender" v-model="gender" id="gender2" value="female" @blur="$v.gender.$touch()">
            <label  for="gender2">Женский</label>
          </span>
    </div>

    <div class="field">
      <label for="passport_data">Серия и номер паспорта</label>
      <input id="passport_data" placeholder="1234 567890" type="text" v-model.trim="passportData" @blur="$v.passportData.$touch()" />
      <div
        class="error"
        v-if="$v.passportData.$error"
      >Серия и номер паспорта должны быть в формате 1234 567890</div>
    </div>

    <div class="field">
      <label for="passport_date">Дата выдачи паспорта</label>
      <input id="passport_date" type="date" v-model="passportDate" @blur="$v.passportDateObj.$touch()" />
      <span class="error" v-if="!$v.passportDateObj.required">*</span>
      <div
        class="error"
        v-if="$v.passportDateObj.$error"
      >Дата выдачи паспорта должна быть прошедшей в формате дд.мм.гггг </div>
    </div>







    <button type="submit" :disabled="$v.$invalid">Отправить форму</button>
  </form>
</template>

<script>
import { required, maxLength, minLength, maxValue, minValue } from "vuelidate/lib/validators";



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
      passportDate: null,
    };
  },
  computed:{
    passportDateObj () {
      return this.passportDate ? new Date(this.passportDate) : null;
    },
    birthdayObj () {
      return this.birthday ? new Date(this.birthday) : null;
    }
  },

  validations: {
    passportData: {
      required,
      validFormat: (val) => /^\d{4} \d{6}$/.test(val),
    },
    passportDateObj: {
      required,
      maxValue: maxValue(new Date()),
      minValue: minValue(new Date(1974, 8,28)),
    },
    birthdayObj: {
      required,
      maxValue: maxValue(new Date()),
      minValue: minValue(new Date(1920, 1,1)),
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
      validFormat: (val) => /^((7) ?)?((\(\d{3}\))|(\d{3}))?(\d{3}?\d{2}?\d{2})$/.test(val),
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
  outline-color: #F99;
}

.valid {
  border-color: #5A5;
  background: #EFE;
}

.valid:focus {
  outline-color: #8E8;
}
</style>
