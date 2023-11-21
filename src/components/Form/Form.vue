<template>
	<form id="form" @submit.prevent="submitForm">
		<div>
			<label for="last-name">Фамилия*</label>
			<input v-model="form.lastName" id="last-name" required>
		</div>
		<div>
			<label for="first-name">Имя*</label>
			<input v-model="form.firstName" id="first-name" required>
		</div>
		<div>
			<label for="middle-name">Отчество</label>
			<input v-model="form.middleName" id="middle-name">
		</div>
		<div>
			<label for="birthdate">Дата рождения*</label>
			<input v-model="form.birthdate" id="birthdate" type="date" required>
		</div>
		<div>
			<label for="phone-number">Номер телефона*</label>
			<input v-model="form.phoneNumber" id="phone-number" pattern="7[0-9]{10}" required>
		</div>
		<div>
			<label for="gender">Пол</label>
			<input v-model="form.gender" id="gender">
		</div>
		<div>
			<label for="customer-group">Группа клиентов*</label>
			<select v-model="form.customerGroup" id="customer-group" multiple required>
				<option value="VIP">VIP</option>
				<option value="Проблемные">Проблемные</option>
				<option value="ОМС">ОМС</option>
			</select>
		</div>
		<div>
			<label for="doctor">Лечащий врач</label>
			<select v-model="form.doctor" id="doctor">
				<option value="Иванов">Иванов</option>
				<option value="Захаров">Захаров</option>
				<option value="Чернышева">Чернышева</option>
			</select>
		</div>
		<div>
			<label for="no-sms">Не отправлять СМС</label>
			<input v-model="form.noSms" id="no-sms" type="checkbox">
		</div>
		<div>
			<label>Адрес:</label>
			<div>
				<label for="index">Индекс</label>
				<input v-model="form.address.index" id="index">
			</div>
			<div>
				<label for="country">Страна</label>
				<input v-model="form.address.country" id="country">
			</div>
			<div>
				<label for="region">Область</label>
				<input v-model="form.address.region" id="region">
			</div>
			<div>
				<label for="city">Город*</label>
				<input v-model="form.address.city" id="city" required>
			</div>
			<div>
				<label for="street">Улица</label>
				<input v-model="form.address.street" id="street">
			</div>
			<div>
				<label for="house">Дом</label>
				<input v-model="form.address.house" id="house">
			</div>
		</div>
		<div>
			<label for="document-type">Тип документа*</label>
			<select v-model="form.passport.type" id="document-type" required>
				<option value="Паспорт">Паспорт</option>
				<option value="Свидетельство о рождении">Свидетельство о рождении</option>
				<option value="Водительское удостоверение">Водительское удостоверение</option>
			</select>
		</div>
		<div>
			<label for="passport-series">Серия</label>
			<input v-model="form.passport.series" id="passport-series">
		</div>
		<div>
			<label for="passport-number">Номер</label>
			<input v-model="form.passport.number" id="passport-number">
		</div>
		<div>
			<label for="passport-issuer">Кем выдан</label>
			<input v-model="form.passport.issuer" id="passport-issuer">
		</div>
		<div>
			<label for="passport-issued-date">Дата выдачи*</label>
			<input v-model="form.passport.issuedDate" id="passport-issued-date" type="date" required>
		</div>
		<button type="submit">Отправить</button>
	</form>
</template>

<script>
import { useVuelidate } from "@vuelidate/core";
import { required, minLength, maxLength, numeric } from '@vuelidate/validators';

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
				customerGroup: [],
				doctor: '',
				noSms: false,
				address: {
					index: '',
					country: '',
					region: '',
					city: '',
					street: '',
					house: ''
				},
				passport: {
					type: '',
					series: '',
					number: '',
					issuer: '',
					issuedDate: ''
				}
			}
		};
	},
	validations: {
		form: {
			lastName: { required },
			firstName: { required },
			birthdate: { required },
			phoneNumber: {
				required,
				numeric,
				minLength: minLength(11),
				maxLength: maxLength(11)
			},
			customerGroup: { required },
			city: { required },
			issuedDate: { required }
		}
	},
	methods: {
		submitForm() {
			console.log("submitForm")
		}
	}
};
</script>  