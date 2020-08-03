<template>
  <div>
     <h2>Шаг {{ step }} из 5</h2>
    
      <div class="field">
        
      <label class="label" for="documents">Выберите документ</label>
      <p class="select">
      <select class="budget" id="documents" v-model="documentsForm.documents">
        <option value="documentsPassport">Паспорт</option>
        <option value="documentsBirth">Свид. о рождении</option>
        <option value="documentsDriver">Вод. удостоверение</option>
      </select>
      </p>
      </div>
    
    <!-- <h2 v-if="documentsForm.documents == 'documentsPassport'">Паспорт</h2>
    <h2 v-else-if="documentsForm.documents == 'documentsBirth'">Свид. о рождении</h2>
    <h2 v-else-if="documentsForm.documents == 'documentsDriver'">Вод. удостоверение</h2> -->
    <template v-if="documentsForm.documents == 'documentsPassport'">
      <div class="field">
        <label class="label" for="passport_serial">Серия паспорта</label>
        <input
          id="passport_serial"
          placeholder="Введите серию паспорта"
          type="text"
          min="0"
          max="9999"
          v-model="documentsForm.passportSerial"
          @blur="v.documentsForm.passportSerial.$touch()"
          :class="{ 'error': v.documentsForm.passportSerial.$error }"
          :maxlength="v.documentsForm.passportSerial.$params.maxLength.max"
        />

        <div
          class="error-message"
          v-if="v.documentsForm.passportSerial.$error"
        >Серия паспорта должна быть числом из 4 знаков</div>
      </div>

      <div class="field">
        <label class="label" for="passport_number">Номер паспорта</label>
        <input
          id="passport_number"
          placeholder="Введите номер паспорта"
          type="text"
          min="0"
          max="999999"
          v-model="documentsForm.passportNumber"
          @blur="v.documentsForm.passportNumber.$touch()"
          :class="{ 'error': v.documentsForm.passportNumber.$error }"
          :maxlength="v.documentsForm.passportNumber.$params.maxLength.max"
        />
        <div
          class="error-message"
          v-if="v.documentsForm.passportNumber.$error"
        >Номер паспорта должен быть числом из 6 знаков</div>
      </div>

      <div class="field">
        <label class="label" for="passport_issued">Выдан</label>
        <textarea
          id="passport_issued"
          placeholder="Введите кем был выдан паспорт, не более 100 символов"
          v-model="v.documentsForm.passportIssued.$model"
          @blur="v.documentsForm.passportIssued.$touch()"
          :maxlength="v.documentsForm.passportIssued.$params.maxLength.max"
          :minlength="v.documentsForm.passportIssued.$params.minLength.min"
        />
        <span
          class="counter"
        >{{ documentsForm.passportIssued.length }} / {{ v.documentsForm.passportIssued.$params.maxLength.max}}</span>
        <div
          class="error-message"
          v-if="v.documentsForm.passportIssued.$error"
        >Длина строки не менее 30 и не более 100 символов</div>
      </div>

      <div class="field">
        <label class="label" for="passport_date">Дата выдачи паспорта</label>
        <input
          id="passport_date"
          type="date"
          v-model="documentsForm.passportDate"
          @blur="v.documentsForm.passportDate.$touch()"
          :class="{ 'error': v.documentsForm.passportDate.$error || !v.documentsForm.passportDate.required }" 
        />
        <div class="error-message" v-if="!v.documentsForm.passportDate.required">Это обязательное поле</div>
        <div
          class="error-message"
          v-if="v.documentsForm.passportDate.$error"
        >Дата выдачи паспорта должна быть прошедшей в формате дд.мм.гггг</div>
      </div>
    </template>
    <template v-if="documentsForm.documents == 'documentsBirth'">
      <div class="field">
        <label class="label" for="birth_serial">Серия свидетельтва</label>
        <input
          id="birth_serial"
          placeholder="Введите серию свидетельсва"
          type="text"
          min="0"
          max="9999"
          v-model="documentsForm.birthSerial"
          @blur="v.documentsForm.birthSerial.$touch()"
          :class="{ 'error': v.documentsForm.birthSerial.$error }"
          :maxlength="v.documentsForm.birthSerial.$params.maxLength.max"
        />
        <div
          class="error-message"
          v-if="v.documentsForm.birthSerial.$error"
        >Первая часть серии содержит римские цифры (от 1 до 4 знаков), вторая часть - две буквы из кириллицы</div>
      </div>

      <div class="field">
        <label class="label" for="birth_number">Номер свидетельства</label>
        <input
          id="birth_number"
          placeholder="Введите номер свидетельтсва"
          type="text"
          min="0"
          max="999999"
          v-model="documentsForm.birthNumber"
          @blur="v.documentsForm.birthNumber.$touch()"
          :class="{ 'error': v.documentsForm.birthNumber.$error }"
          :maxlength="v.documentsForm.birthNumber.$params.maxLength.max"
        />
        <div
          class="error-message"
          v-if="v.documentsForm.birthNumber.$error"
        >Номер свидетельсва должен быть числом из 6 знаков</div>
      </div>

      <div class="field">
        <label class="label" for="birth_issued">Выдано</label>
        <textarea
          id="birth_issued"
          placeholder="Введите кем было выдано свидетельтво, не более 100 символов"
          v-model="v.documentsForm.birthIssued.$model"
          @blur="v.documentsForm.birthIssued.$touch()"
          :maxlength="v.documentsForm.birthIssued.$params.maxLength.max"
          :minlength="v.documentsForm.birthIssued.$params.minLength.min"
        />
        <span
          class="counter"
        >{{ documentsForm.birthIssued.length }} / {{ v.documentsForm.birthIssued.$params.maxLength.max}}</span>
        <div
          class="error-message"
          v-if="v.documentsForm.birthIssued.$error"
        >Длина строки не менее 30 и не более 100 символов</div>
      </div>

      <div class="field">
        <label class="label" for="birth_date">Дата выдачи свидетельства</label>
        <input
          id="birth_date"
          type="date"
          v-model="documentsForm.birthDate"
          @blur="v.documentsForm.birthDate.$touch()"
          :class="{ 'error': v.documentsForm.birthDate.$error || !v.documentsForm.birthDate.required }"
        />
        <div class="error-message" v-if="!v.documentsForm.birthDate.required">Это обязательное поле</div>
        <div
          class="error-message"
          v-if="v.documentsForm.birthDate.$error"
        >Дата выдачи свидетельства должна быть прошедшей в формате дд.мм.гггг</div>
      </div>
    </template>


    <template v-if="documentsForm.documents == 'documentsDriver'">
      <div class="field">
        <label class="label" for="driver_serial">Серия удостоверения</label>
        <input
          id="driver_serial"
          placeholder="Введите серию удостоверения"
          type="text"
          min="0"
          max="9999"
          v-model="documentsForm.driverSerial"
          @blur="v.documentsForm.driverSerial.$touch()"
          :class="{ 'error': v.documentsForm.driverSerial.$error }"
          :maxlength="v.documentsForm.driverSerial.$params.maxLength.max"
        />
        <div
          class="error-message"
          v-if="v.documentsForm.driverSerial.$error"
        >Серия удостоверения состоит из четырех цифр</div>
      </div>

      <div class="field">
        <label class="label" for="driver_number">Номер удостоверения</label>
        <input
          id="driver_number"
          placeholder="Введите номер удостоверения"
          type="text"
          min="0"
          max="999999"
          v-model="documentsForm.driverNumber"
          @blur="v.documentsForm.driverNumber.$touch()"
          :class="{ 'error': v.documentsForm.driverNumber.$error }"
          :maxlength="v.documentsForm.driverNumber.$params.maxLength.max"
        />
        <div
          class="error-message"
          v-if="v.documentsForm.driverNumber.$error"
        >Номер удостоверения состоит из 6 цифр</div>
      </div>

      <div class="field">
        <label class="label" for="driver_issued">Выдано</label>
        <textarea
          id="driver_issued"
          placeholder="Введите кем было выдано удостоверение, не более 100 символов"
          v-model="v.documentsForm.driverIssued.$model"
          @blur="v.documentsForm.driverIssued.$touch()"
          :maxlength="v.documentsForm.driverIssued.$params.maxLength.max"
          :minlength="v.documentsForm.driverIssued.$params.minLength.min"
        />
        <span
          class="counter"
        >{{ documentsForm.driverIssued.length }} / {{ v.documentsForm.driverIssued.$params.maxLength.max}}</span>
        <div
          class="error-message"
          v-if="v.documentsForm.driverIssued.$error"
        >Длина строки не менее 30 и не более 100 символов</div>
      </div>

      <div class="field">
        <label class="label" for="driver_date">Дата выдачи удостоверения</label>
        <input
          id="driver_date"
          type="date"
          v-model="documentsForm.driverDate"
          @blur="v.documentsForm.driverDate.$touch()"
          :class="{ 'error': v.documentsForm.driverDate.$error || !v.documentsForm.driverDate.required }"
        />
        <div class="error-message" v-if="!v.documentsForm.driverDate.required">Это обязательное поле</div>
        <div
          class="error-message"
          v-if="v.documentsForm.driverDate.$error"
        >Дата выдачи удостоверения должна быть прошедшей в формате дд.мм.гггг</div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: "PassportComponent",
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
    documentsForm: {
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
