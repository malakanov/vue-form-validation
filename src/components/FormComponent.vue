<template>
  <div>
    <form class="vue-form" @submit.prevent="submit">
        <!-- <img width="25%" src="../assets/logo.png"> -->
        <div v-show="step === 1" class="container">
          <client-component v-model="clientForm" v-bind:v="$v" v-bind:step="step" />
          <div class="vue-form-nav">
            <button @click.prevent="next()" :disabled="$v.clientForm.$invalid" >Вперёд</button>
          </div>
        </div>
        <div v-show="step === 2" class="container">
          <contacts-component v-model="contactsForm" v-bind:v="$v" v-bind:step="step" />
          <div class="vue-form-nav">
            <button @click.prevent="prev()">Назад</button>
            <button @click.prevent="next()" :disabled="$v.contactsForm.$invalid">Вперёд</button>
          </div>
        </div>
        <div v-show="step === 3" class="container">
          <adress-component v-model="adressForm" v-bind:v="$v" v-bind:step="step" />
          <div class="vue-form-nav">
            <button @click.prevent="prev()">Назад</button>
            <button @click.prevent="next()">Вперёд</button>
          </div>
        </div>
        <div v-show="step === 4" class="container">
          <building-component v-model="buildingForm" v-bind:v="$v" v-bind:step="step" />
          <div class="vue-form-nav">
            <button @click.prevent="prev()">Назад</button>
            <button @click.prevent="next()" :disabled="$v.buildingForm.$invalid">Вперёд</button>
          </div>
        </div>
        <div v-show="step === 5" class="container">
          <documents-component v-model="documentsForm" v-bind:v="$v" v-bind:step="step" />
          <div class="vue-form-nav">
            <button @click.prevent="prev()">Назад</button>
            <button type="submit" >Отправить форму</button>
          </div>
        </div>
    </form>
  </div>
</template>

<script>
import {
  required,
  maxLength,
  minLength,
  maxValue,
  minValue,
  numeric,
} from "vuelidate/lib/validators";
import ClientComponent from "@/components/ClientComponent";
import ContactsComponent from "@/components/ContactsComponent";
import DocumentsComponent from "@/components/DocumentsComponent";
import AdressComponent from "@/components/AdressComponent";
import BuildingComponent from "@/components/BuildingComponent";

export default {
  name: "FormComponent",
  components: {
    ClientComponent,
    ContactsComponent,
    DocumentsComponent,
    AdressComponent,
    BuildingComponent,
  },
  data() {
    return {
      clientForm: {
        firstName: null,
        lastName: null,
        middleName: "",
        birthday: null,
      },
      contactsForm:{
        phone: null,
        gender: null,
        multipleSelections: [],
        assets: ["VIP", "Проблемные", "ОМС"],
        doctor: null,
        sms: null,
      },
      adressForm: {
        index: null,
        country: null,
        region: null,
      },
      buildingForm: {
        city: null,
        street: "",
        building: "",
      },
      documentsForm: {
        documents: "",
        passportSerial: null,
        passportNumber: null,
        passportDate: null,
        passportIssued: "",
        birthSerial: null,
        birthNumber: null,
        birthDate: null,
        birthIssued: "",
        driverSerial: null,
        driverNumber: null,
        driverDate: null,
        driverIssued: "",
      },
      step: 1,
    };
  },
  computed: {},

  validations: {
    clientForm: {
      lastName: {
        required,
        maxLength: maxLength(30),
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      firstName: {
        required,
        maxLength: maxLength(30),
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      middleName: {
        maxLength: maxLength(30),
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
      birthday: {
        required,
        maxValue: (value) => value < new Date().toISOString(),
        minValue: (value) => value > new Date(1920, 1, 1).toISOString(),
      },
    },
    contactsForm: {
      phone: {
        required,
        maxLength: maxLength(12),
        mixLength: minLength(11),
        validFormat: (val) =>
          /^((7) ?)?((\(\d{3}\))|(\d{3}))?(\d{3}?\d{2}?\d{2})$/.test(val),
      },
      multipleSelections: {
        required,
      },
    },
    adressForm: {
      index: {
        validFormat: (val) => /^\d{6}$/.test(val),
      },
      country: {
        maxLength: maxLength(35),
        alpha: (val) =>
          /^[А-Я]{1}[А-Яа-я]{2}([-А-Яа-я]{0,2})?([-А-Яа-я’]{0,1})?([-А-Яа-яё]{0,2})?([А-Яа-я]{0,1})?([а-я]{0,12})?( [(А-Яа-я–]{1})?([А-Яа-я]{0,1})?([а-я]{0,8})?( [А-Я]{1})?([а-я]{4})?([)а-я]{0,1})?([а-я]{0,9})?( [А-Я]{1})?([а-я]{5,9})?$/i.test(
            val
          ),
      },
      region: {
        maxLength: maxLength(50),
        alpha: (val) => /^[а-яё]*$/i.test(val),
      },
    },
    buildingForm: {
      city: {
        required,
        maxLength: maxLength(35),
        alpha: (val) => /^[а-яё]+((?:[- ][а-яё]+)*)+$/i.test(val),
      },
      street: {
        maxLength: maxLength(50),
        // alphaNum: (val) =>
        //   /^[0-9А-Я]{1}([0-9А-Яа-я]{0,1})?([А-Яа-я]{0,1})?([а-я]{0,14})?( [0-9А-Яа-я]{1,2})?([-А-Яа-я]{0,1})?([а-я]{0,4})?([-а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,2})?([-а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,1})?( [0-9А-Яа-я]{1})?([А-Яа-я]{0,3})?([а-я]{0,6})?([-а-я]{0,1})?([-0-9а-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,2})?( [(0-9А-Яа-я]{1})?([0-9а-я]{1})?([А-Яа-я]{0,1})?([0-9а-я]{0,1})?([а-я]{0,3})?([)а-я]{0,1})?( [0-9А-Яа-я]{1})?([0-9а-я]{0,1})?(.{0,1})?([0-9а-я]{0,2})?([а-я]{0,3})?$/i.test(
        //     val
        //   ),
      },
      building: {
        // validFormat: (val) =>
        //   /^[1-9]\d*(?: ?(?:[А-Яа-я]|[/-] ?\d?))?$/.test(val),
      },
    },
    documentsForm: {
      passportDate: {
        required,
        maxValue: (value) => value < new Date().toISOString(),
        minValue: (value) => value > new Date(1974, 8, 28).toISOString(),
        // maxValue: maxValue(new Date()),
        // minValue: minValue(new Date(1974, 8, 28)),
      },
      passportSerial: {
        numeric,
        maxLength: maxLength(4),
        minLength: minLength(4),
        maxValue: maxValue(9999),
        minValue: minValue(0),
      },
      passportNumber: {
        numeric,
        maxLength: maxLength(6),
        minLength: minLength(6),
        maxValue: maxValue(999999),
        minValue: minValue(0),
      },
      passportIssued: {
        maxLength: maxLength(100),
        minLength: minLength(30),
      },
      birthDate: {
        required,
        maxValue: (value) => value < new Date().toISOString(),
        minValue: (value) => value > new Date(1920, 1, 1).toISOString(),
        // maxValue: maxValue(new Date()),
        // minValue: minValue(new Date(1920, 1, 1)),
      },
      birthSerial: {
        maxLength: maxLength(7),
        minLength: minLength(4),
        validFormat: (val) =>
          /^M{0,3}(D?C{0,3}|C[DM])(L?X{0,3}|X[LC])(V?I{0,3}|I[VX])((?<!^)-)?[\u0410-\u044F]{2}$/.test(
            val
          ),
      },
      birthNumber: {
        numeric,
        maxLength: maxLength(6),
        minLength: minLength(6),
        maxValue: maxValue(999999),
        minValue: minValue(0),
      },
      birthIssued: {
        maxLength: maxLength(100),
        minLength: minLength(30),
      },
      driverDate: {
        required,
        maxValue: (value) => value < new Date().toISOString(),
        minValue: (value) => value > new Date(1920, 1, 1).toISOString(),
        // maxValue: maxValue(new Date()),
        // minValue: minValue(new Date(1920, 1, 1)),
      },
      driverSerial: {
        numeric,
        maxLength: maxLength(4),
        minLength: minLength(4),
        maxValue: maxValue(9999),
        minValue: minValue(0),
      },
      driverNumber: {
        numeric,
        maxLength: maxLength(6),
        minLength: minLength(6),
        maxValue: maxValue(999999),
        minValue: minValue(0),
      },
      driverIssued: {
        maxLength: maxLength(100),
        minLength: minLength(30),
      },
    },
  },

  methods: {
    submit() {
      this.$v.$touch();
      if(this.$v.$invalid) return
      // to form submit after this
      alert('Form submitted')
    },
    prev() {
      this.step--;
    },
    next() {
      this.step++;
    },
  },
};
</script>
