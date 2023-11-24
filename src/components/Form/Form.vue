<template>
  <form id="form" @submit.prevent="submitForm">
    <div class="form__page" v-if="currentStep === 1">
      <h3>Персональные данные</h3>
      <div class="page__field">
        <label for="last-name">Фамилия*</label>
        <input v-model="form.pageOne.lastName" id="last-name" required placeholder="Иванов"
               @blur="v$.form.pageOne.lastName.$touch"
               maxlength="50">
        <div class="error--message" v-if="v$.form.pageOne.lastName.$errors.length">
          <span v-if="v$.form.pageOne.lastName.required.$invalid">
            Поле "Фамилия" обязательно для заполнения
          </span>
          <span v-else-if="v$.form.pageOne.lastName.isValidTextField.$invalid">
            Поле "Фамилия" содержит недопустимые символы
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="first-name">Имя*</label>
        <input v-model="form.pageOne.firstName" id="first-name" required placeholder="Иван"
               @blur="v$.form.pageOne.firstName.$touch"
               maxlength="50">
        <div class="error--message" v-if="v$.form.pageOne.firstName.$errors.length">
          <span v-if="v$.form.pageOne.firstName.isValidTextField.$invalid">
            Поле "Имя" содержит недопустимые символы
          </span>
          <span v-else-if="v$.form.pageOne.firstName.required.$invalid">
            Поле "Имя" обязательно для заполнения
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="middle-name">Отчество</label>
        <input v-model="form.pageOne.middleName" id="middle-name" placeholder="Иванович" maxlength="50"
               @blur="v$.form.pageOne.middleName.$touch">
        <div class="error--message" v-if="v$.form.pageOne.middleName.$errors.length">
          <span v-if="v$.form.pageOne.middleName.isValidTextField.$invalid">
            Поле "Отчество" содержит недопустимые символы
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="birthdate">Дата рождения*</label>
        <input v-model="form.pageOne.birthdate" id="birthdate" type="date" required
               @blur="v$.form.pageOne.birthdate.$touch"
               maxlength="8">
        <div class="error--message" v-if="v$.form.pageOne.birthdate.$errors.length">
         <span v-if="v$.form.pageOne.birthdate.required.$invalid">
           Поле "Дата рождения" обязательно для заполнения
         </span>
          <span v-else-if="v$.form.pageOne.birthdate.isValidDate.$invalid">
           Некорректно введенная дата (дата не может быть больше текущей)
         </span>
        </div>
      </div>
      <div class="page__field">
        <label for="phone-number">Номер телефона*</label>
        <input v-model="form.pageOne.phoneNumber" id="phone-number"
               pattern="7[0-9]{10}"
               type="tel"
               placeholder="79999999999"
               @blur="v$.form.pageOne.phoneNumber.$touch"
               minlength="11"
               maxlength="11"
               required>
        <div class="error--message" v-if="v$.form.pageOne.phoneNumber.$errors.length">
          <span
              v-if="v$.form.pageOne.phoneNumber.required.$invalid">
            Поле "Номер телефона" обязательно для заполнения
          </span>
          <span
              v-else-if="v$.form.pageOne.phoneNumber.numeric.$invalid">
            Поле "Номер телефона" должно содержать только цифры
          </span>
          <span v-else-if="v$.form.pageOne.phoneNumber.minLength.$invalid">
            Поле "Номер телефона" должно содержать 11 цифр
          </span>
          <span
              v-else-if="v$.form.pageOne.phoneNumber.isValidPhoneNumber.$invalid">
            Некорректно введенный номер телефона
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="gender">Пол</label>
        <select v-model="form.pageOne.gender" id="gender">
          <option value="Мужской">Мужской</option>
          <option value="Женский">Женский</option>
        </select>
      </div>
      <div class="page__field">
        <label for="customer-group">Группа клиентов*</label>
        <select v-model="form.pageOne.customerGroup" id="customer-group" @blur="v$.form.pageOne.customerGroup.$touch"
                multiple required size="2">
          <option value="VIP">VIP</option>
          <option value="Проблемные">Проблемные</option>
          <option value="ОМС">ОМС</option>
        </select>
        <div class="error--message" v-if="v$.form.pageOne.customerGroup.$errors.length">
          Поле "Группа клиентов" обязательно для заполнения
        </div>
      </div>
      <div class="page__field">
        <label for="doctor">Лечащий врач</label>
        <select v-model="form.pageOne.doctor" id="doctor">
          <option value="Иванов">Иванов</option>
          <option value="Захаров">Захаров</option>
          <option value="Чернышева">Чернышева</option>
        </select>
      </div>
      <div class="page__field">
        <label for="no-sms">Не отправлять СМС</label>
        <input v-model="form.pageOne.noSms" id="no-sms" type="checkbox">
      </div>
    </div>

    <div class="form__page" v-if="currentStep === 2">
      <h3>Адрес</h3>
      <div class="page__field">
        <label for="index">Индекс</label>
        <input v-model="form.pageTwo.index" id="index" placeholder="101000" maxlength="6"
               @blur="v$.form.pageTwo.index.$touch">
        <div class="error--message" v-if="v$.form.pageTwo.index.$errors.length">
          <span v-if="v$.form.pageTwo.index.numeric.$invalid">Поле "Индекс" должно содержать только цифры</span>
          <span v-else-if="v$.form.pageTwo.index.minLength.$invalid">Поле "Индекс" должно содержать 6 цифр</span>
        </div>
      </div>
      <div class="page__field">
        <label for="country">Страна</label>
        <input v-model="form.pageTwo.country" id="country" placeholder="Россия" maxlength="30"
               @blur="v$.form.pageTwo.country.$touch">
        <div class="error--message" v-if="v$.form.pageTwo.country.$errors.length">
          <span v-if="v$.form.pageTwo.country.isValidTextField.$invalid">
            Поле "Страна" содержит недопустимые символы
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="region">Область</label>
        <input v-model="form.pageTwo.region" id="region" placeholder="Московская область" maxlength="50"
               @blur="v$.form.pageTwo.region.$touch">
        <div class="error--message" v-if="v$.form.pageTwo.region.$errors.length">
          <span v-if="v$.form.pageTwo.region.isValidTextField.$invalid">
            Поле "Область" содержит недопустимые символы
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="city">Город*</label>
        <input v-model="form.pageTwo.city" id="city" required placeholder="Москва" maxlength="60"
               @blur="v$.form.pageTwo.city.$touch">
        <div class="error--message" v-if="v$.form.pageTwo.city.$errors.length">
          <span v-if="v$.form.pageTwo.city.required.$invalid">
            Поле "Город" обязательно для заполнения
          </span>
          <span v-else-if="v$.form.pageTwo.city.isValidTextField.$invalid">
            Поле "Город" содержит недопустимые символы
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="street">Улица</label>
        <input v-model="form.pageTwo.street" id="street" placeholder="Московское шоссе" maxlength="80">
      </div>
      <div class="page__field">
        <label for="house">Дом</label>
        <input v-model="form.pageTwo.house" id="house" placeholder="д. 1" maxlength="20">
      </div>
    </div>

    <div class="form__page" v-if="currentStep === 3">
      <h3>Документы</h3>
      <div class="page__field">
        <label for="document-type">Тип документа*</label>
        <select v-model="form.pageThree.type" id="document-type" required @blur="v$.form.pageThree.type.$touch">
          <option value="Паспорт">Паспорт</option>
          <option value="Свидетельство о рождении">Свидетельство о рождении</option>
          <option value="Водительское удостоверение">Водительское удостоверение</option>
        </select>
        <div class="error--message" v-if="v$.form.pageThree.type.$errors.length">
          <span v-if="v$.form.pageThree.type.required.$invalid">
            Поле "Тип документа" обязательно для заполнения
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="passport-series">Серия</label>
        <input v-model="form.pageThree.series" id="passport-series" placeholder="1234" maxlength="4"
               @blur="v$.form.pageThree.series.$touch">
        <div class="error--message" v-if="v$.form.pageThree.series.$errors.length">
          <span v-if="v$.form.pageThree.series.numeric.$invalid">
            Поле "Серия" должно содержать только цифры
          </span>
          <span v-else-if="v$.form.pageThree.series.minLength.$invalid">
            Поле "Серия" должно содержать не менее 4 цифр
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="passport-number">Номер</label>
        <input v-model="form.pageThree.number" id="passport-number" placeholder="123456" maxlength="6"
               @blur="v$.form.pageThree.number.$touch">
        <div class="error--message" v-if="v$.form.pageThree.number.$errors.length">
          <span v-if="v$.form.pageThree.number.numeric.$invalid">
            Поле "Номер" должно содержать только цифры
          </span>
          <span v-else-if="v$.form.pageThree.number.minLength.$invalid">
            Поле "Номер" должно содержать не менее 6 цифр
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="passport-issuer">Кем выдан</label>
        <input v-model="form.pageThree.issuer" id="passport-issuer" maxlength="80"
               @blur="v$.form.pageThree.issuer.$touch">
        <div class="error--message" v-if="v$.form.pageThree.issuer.$errors.length">
          <span v-if="v$.form.pageThree.issuer.isValidTextField.$invalid">
          Поле "Кем выдан" содержит недопустимые символы
          </span>
        </div>
      </div>
      <div class="page__field">
        <label for="passport-issued-date">Дата выдачи*</label>
        <input v-model="form.pageThree.issuedDate" id="passport-issued-date" type="date" maxlength="8" required
               @blur="v$.form.pageThree.issuedDate.$touch">
        <div class="error--message" v-if="v$.form.pageThree.issuedDate.$errors.length">
          <span v-if="v$.form.pageThree.issuedDate.required.$invalid">
            Поле "Дата выдачи" обязательно для заполнения
          </span>
          <span v-else-if="v$.form.pageThree.issuedDate.isValidDate.$invalid">
            Некорректно введенная дата (дата не может быть больше текущей)
          </span>
        </div>
      </div>
    </div>


    <div class="stepBtnGroup">
      <button type="button" @click="previousStep" v-bind:disabled="currentStep <= 1">Назад</button>
      <button type="button" @click="nextStep" v-bind:disabled="currentStep >= 3">Далее</button>
    </div>
    <button type="submit" v-if="currentStep === 3">Отправить</button>
    <span class="form--message">* - обязательные поля</span>
  </form>
</template>

<style lang="sass">
@import "./Form.sass"
</style>

<script>
import {useVuelidate} from "@vuelidate/core";
import {required, minLength, numeric,} from '@vuelidate/validators';

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
        pageOne: {
          lastName: '',
          firstName: '',
          middleName: '',
          birthdate: '',
          phoneNumber: '',
          gender: '',
          customerGroup: [],
          doctor: '',
          noSms: false,
        },
        pageTwo: {
          index: '',
          country: '',
          region: '',
          city: '',
          street: '',
          house: ''
        },
        pageThree: {
          type: '',
          series: '',
          number: '',
          issuer: '',
          issuedDate: ''
        },
      },
      currentStep: 3
    };
  },
  validations() {
    return {
      form: {
        pageOne: {
          lastName: {
            required,
            isValidTextField: text => this.isValidTextField(text)
          },
          firstName: {
            required,
            isValidTextField: text => this.isValidTextField(text)
          },
          middleName: {
            isValidTextField: text => this.isValidTextField(text)
          },
          birthdate: {
            required,
            isValidDate: date => this.isValidDate(date)
          },
          phoneNumber: {
            required,
            isValidPhoneNumber: number => this.isValidPhoneNumber(number),
            minLength: minLength(11),
            numeric
          },
          customerGroup: {
            required
          },
        },
        pageTwo: {
          index: {
            numeric,
            minLength: minLength(6)
          },
          country: {
            isValidTextField: text => this.isValidTextField(text)
          },
          region: {
            isValidTextField: text => this.isValidTextField(text)
          },
          city: {
            required,
            isValidTextField: text => this.isValidTextField(text)
          },
          street: {
            isValidTextField: text => this.isValidTextField(text)
          },
        },
        pageThree: {
          type: {
            required
          },
          series: {
            numeric,
            minLength: minLength(4)
          },
          number: {
            numeric,
            minLength: minLength(6)
          },
          issuer: {
            isValidTextField: text => this.isValidTextField(text)
          },
          issuedDate: {
            required,
            isValidDate: date => this.isValidDate(date)
          }
        }
      }
    }
  },
  methods: {
    async submitForm() {
      if (this.v$.$invalid) {
        this.v$.$touch();
        this.currentStep = 1;
      } else
        console.log("Form submitted: ", this.form)
    },
    nextStep() {
      if (this.isValidPage(this.currentStep))
        this.currentStep++
      else
        this.v$.$touch()
    },
    previousStep() {
      this.currentStep--
    },
    isValidDate(date) {
      const currentDate = new Date();
      const selectedDate = new Date(date);

      // Сравнение годов
      if (currentDate.getFullYear() < selectedDate.getFullYear()) {
        return false;
      }

      // Сравнение месяцев, если годы равны
      if (currentDate.getFullYear() === selectedDate.getFullYear() &&
          currentDate.getMonth() < selectedDate.getMonth()) {
        return false;
      }

      // Сравнение дней, если годы и месяцы равны
      if (currentDate.getFullYear() === selectedDate.getFullYear() &&
          currentDate.getMonth() === selectedDate.getMonth() &&
          currentDate.getDate() < selectedDate.getDate()) {
        return false;
      }

      return true;
    },
    isValidPhoneNumber(phoneNumber) {
      return /^7[0-9]{10}$/.test(phoneNumber);
    },
    isValidTextField(text) {
      if (text === '')
        return true
      const reg = /^[а-яА-Я-a-zA-Z\s]+$/
      return reg.test(text)
    },
    isValidPage(page) {
      switch (page) {
        case 1:
          return !this.v$.form.pageOne.$invalid
        case 2:
          return !this.v$.form.pageTwo.$invalid
        case 3:
          return !this.v$.form.pageThree.$invalid
      }
    }
  }
};
</script>