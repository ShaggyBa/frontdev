<template>
  <form id="form" @submit.prevent="submitForm">
    <div class="form__page" v-if="currentStep === 1">
      <h3>Персональные данные</h3>
      <div class="page__field">
        <label for="last-name">Фамилия*</label>
        <input v-model="form.lastName" id="last-name" required placeholder="Иванов"
               @blur="v$.form.lastName.$touch"
               maxlength="50">
        <div class="error--message" v-if="v$.form.lastName.$error">
          Поле "Фамилия" обязательно для заполнения
        </div>
      </div>
      <div class="page__field">
        <label for="first-name">Имя*</label>
        <input v-model="form.firstName" id="first-name" required placeholder="Иван"
               @blur="v$.form.firstName.$touch"
               maxlength="50">
        <div class="error--message" v-if="v$.form.firstName.$error">
          Поле "Имя" обязательно для заполнения
        </div>
      </div>
      <div class="page__field">
        <label for="middle-name">Отчество</label>
        <input v-model="form.middleName" id="middle-name" placeholder="Иванович" maxlength="50">
      </div>
      <div class="page__field">
        <label for="birthdate">Дата рождения*</label>
        <input v-model="form.birthdate" id="birthdate" type="date" required
               @blur="v$.form.birthdate.$touch"
               maxlength="8">
        <div class="error--message" v-if="v$.form.birthdate.$error">
          <template v-if="v$.form.birthdate.$params.required">
            Поле "Дата рождения" обязательно для заполнения.
          </template>
          <template v-else-if="v$.form.birthdate.$params.type === 'isValidDate'">
            Поле "Дата рождения" должно быть действительной датой.
          </template>
        </div>
      </div>
      <div class="page__field">
        <label for="phone-number">Номер телефона*</label>
        <input v-model="form.phoneNumber" id="phone-number"
               pattern="7[0-9]{10}"
               type="tel"
               placeholder="79999999999"
               :class="{ 'invalid': v$.form.phoneNumber.$dirty && v$.form.phoneNumber.$error }"
               @blur="v$.form.phoneNumber.$touch"
               minlength="11"
               maxlength="11"
               required>
        <div class="error--message" v-if="v$.form.phoneNumber.$error">
         <span v-for="error in v$.form.phoneNumber.$errors" :key="error.$uid"> {{ error.$message }}</span>
        </div>
      </div>
      <div class="page__field">
        <label for="gender">Пол</label>
        <select v-model="form.gender" id="gender">
          <option value="Мужской">Мужской</option>
          <option value="Женский">Женский</option>
        </select>
      </div>
    </div>

    <div class="form__page" v-if="currentStep === 2">
      <h3>Персональные данные 2</h3>
      <div class="page__field">
        <label for="customer-group">Группа клиентов*</label>
        <select v-model="form.customerGroup" id="customer-group" multiple required>
          <option value="VIP">VIP</option>
          <option value="Проблемные">Проблемные</option>
          <option value="ОМС">ОМС</option>
        </select>
      </div>
      <div class="page__field">
        <label for="doctor">Лечащий врач</label>
        <select v-model="form.doctor" id="doctor">
          <option value="Иванов">Иванов</option>
          <option value="Захаров">Захаров</option>
          <option value="Чернышева">Чернышева</option>
        </select>
      </div>
      <div class="page__field">
        <label for="no-sms">Не отправлять СМС</label>
        <input v-model="form.noSms" id="no-sms" type="checkbox">
      </div>
    </div>

    <div class="form__page" v-if="currentStep === 3">
      <h3>Адрес</h3>
      <div class="page__field">
        <label for="index">Индекс</label>
        <input v-model="form.address.index" id="index" placeholder="101000">
      </div>
      <div class="page__field">
        <label for="country">Страна</label>
        <input v-model="form.address.country" id="country" placeholder="Россия">
      </div>
      <div class="page__field">
        <label for="region">Область</label>
        <input v-model="form.address.region" id="region" placeholder="Московская область">
      </div>
      <div class="page__field">
        <label for="city">Город*</label>
        <input v-model="form.address.city" id="city" required placeholder="г. Москва">
      </div>
      <div class="page__field">
        <label for="street">Улица</label>
        <input v-model="form.address.street" id="street" placeholder="ул. Московское шоссе">
      </div>
      <div class="page__field">
        <label for="house">Дом</label>
        <input v-model="form.address.house" id="house" placeholder="д. 1">
      </div>
    </div>

    <div class="form__page" v-if="currentStep === 4">
      <h3>Документы</h3>
      <div class="page__field">
        <label for="document-type">Тип документа*</label>
        <select v-model="form.passport.type" id="document-type" required>
          <option value="Паспорт">Паспорт</option>
          <option value="Свидетельство о рождении">Свидетельство о рождении</option>
          <option value="Водительское удостоверение">Водительское удостоверение</option>
        </select>
      </div>
      <div class="page__field">
        <label for="passport-series">Серия</label>
        <input v-model="form.passport.series" id="passport-series">
      </div>
      <div class="page__field">
        <label for="passport-number">Номер</label>
        <input v-model="form.passport.number" id="passport-number">
      </div>
      <div class="page__field">
        <label for="passport-issuer">Кем выдан</label>
        <input v-model="form.passport.issuer" id="passport-issuer">
      </div>
      <div class="page__field">
        <label for="passport-issued-date">Дата выдачи*</label>
        <input v-model="form.passport.issuedDate" id="passport-issued-date" type="date" required>
      </div>
    </div>


    <div class="stepBtnGroup">
      <button type="button" @click="previousStep" v-bind:disabled="currentStep <= 1">Назад</button>
      <button type="button" @click="nextStep" v-bind:disabled="currentStep >= 4">Далее</button>
    </div>
    <button type="submit" v-if="currentStep === 1">Отправить</button>
    <span class="form--message">* - обязательные поля</span>
  </form>
</template>

<style lang="sass">
@import "./Form.sass"
</style>

<script>
import {useVuelidate} from "@vuelidate/core";
import {required, minLength, maxLength, numeric,} from '@vuelidate/validators';

export default {
  name: "testForm",
  setup() {
    return {
      v$: useVuelidate()
    }
  },

  data() {
    return {
      form: {
        lastName: '',
        firstName: '',
        middleName: '',
        birthdate: '',
        phoneNumber: '',
        gender: '',
        // customerGroup: [],
        // doctor: '',
        // noSms: false,
        // address: {
        //   index: '',
        //   country: '',
        //   region: '',
        //   city: '',
        //   street: '',
        //   house: ''
        // },
        // passport: {
        //   type: '',
        //   series: '',
        //   number: '',
        //   issuer: '',
        //   issuedDate: ''
        // }
      },
      currentStep: 1
    };
  },
  validations() {
    return {
      form: {
        lastName: {required},
        firstName: {required},
        birthdate: {
          required,
          isValidDate: date => this.isValidDate(date)
        },
        phoneNumber: {
          required,
          numeric,
          regex: /^7[0-9]{10}$/,
          minLength: minLength(11),
          maxLength: maxLength(11),
        },
        // customerGroup: {required},
        // city: {required},
        // issuedDate: {required}
      }
    }
  },
  methods: {
    async submitForm() {
      const result = await this.v$.$validate();
      console.log("submitForm", result)
    },
    nextStep() {
      this.currentStep++
    },
    previousStep() {
      this.currentStep--
    },
    isValidDate(date) {
      const currentDate = new Date();
      const selectedDate = new Date(date)
      return currentDate.getFullYear() >= selectedDate.getFullYear()
    },
  }
};
</script>