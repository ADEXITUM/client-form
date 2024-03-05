<template>
  <div id="app">
    <form @submit.prevent="submitForm" novalidate>
      <div class="main-title-container">
        <medical-icon></medical-icon>
        <h1>Форма создания клиента</h1>
        <medical-icon></medical-icon>
      </div>
      <div class="title-container">
        <h2>Клиент</h2>
        <clientIcon></clientIcon>
      </div>
      <div class="container">
        <div>
          <label for="surname">Фамилия*</label>
          <input type="text" id="surname" @blur="$v.userForm.surname.$touch()" v-model="userForm.surname" :class="{ 'error-input': $v.userForm.surname.$error && $v.userForm.surname.$dirty }">
          <transition name="fade">
          <div v-if="$v.userForm.surname.$error && $v.userForm.surname.$dirty" class="error-message">Фамилия -
            обязательное поле для заполнения
          </div>
          </transition>
        </div>
        <div>
          <label for="name">Имя*</label>
          <input type="text" v-model="userForm.name" id="name" name="name" @blur="$v.userForm.name.$touch()" :class="{ 'error-input': $v.userForm.name.$error && $v.userForm.name.$dirty }"/>
          <transition name="fade">
          <div v-if="$v.userForm.name.$error && $v.userForm.name.$dirty" class="error-message">Имя - обязательное поле
            для заполнения
          </div>
          </transition>
        </div>
        <div>
          <label for="patronymic">Отчество</label>
          <input type="text" id="patronymic" v-model="userForm.patronymic">
        </div>
        <div>
          <label for="birthdate">Дата рождения*</label>
          <input type="date" id="birthdate" @blur="$v.userForm.birthdate.$touch()" v-model="userForm.birthdate" :class="{ 'error-input': $v.userForm.birthdate.$error && $v.userForm.birthdate.$dirty }">
          <transition name="fade">
          <div v-if="$v.userForm.birthdate.$error && $v.userForm.birthdate.$dirty" class="error-message">Дата рождения -
            обязательное поле для заполнения
          </div>
          </transition>
        </div>
        <div>
          <label for="phone">Номер телефона*</label>
          <input type="tel" id="phone" @blur="$v.userForm.phone.$touch()" :class="{ 'error-input': $v.userForm.phone.$error && $v.userForm.phone.$dirty }" v-model="userForm.phone">
          <transition name="fade">
          <div v-if="$v.userForm.phone.$error && $v.userForm.phone.$dirty" class="error-message">Необходимо ввести
            корректный номер телефона
          </div>
          </transition>
        </div>
        <div>
          <label>Пол</label>
          <input type="radio" id="male" value="male" v-model="userForm.gender" name="gender"> Мужской
          <input type="radio" id="female" value="female" v-model="userForm.gender" name="gender"> Женский
        </div>
        <div>
          <label for="clientGroup">Группа клиентов*</label>
          <select id="clientGroup" v-model="userForm.clientGroup" @blur="$v.userForm.clientGroup.$touch()" :class="{ 'error-input': $v.userForm.clientGroup.$error && $v.userForm.clientGroup.$dirty }" multiple>
            <option value="VIP">VIP</option>
            <option value="Проблемные">Проблемные</option>
            <option value="ОМС">ОМС</option>
          </select>
          <transition name="fade">
          <div v-if="$v.userForm.clientGroup.$error && $v.userForm.clientGroup.$dirty" class="error-message">Группа
            клиентов - обязательное поле для заполнения
          </div>
          </transition>
        </div>
        <div>
          <label for="attendingDoctor">Лечащий врач</label>
          <select v-model="userForm.attendingDoctor">
            <option value="Иванов">Иванов</option>
            <option value="Захаров">Захаров</option>
            <option value="Чернышева">Чернышева</option>
          </select>
        </div>
        <div>
          <input type="checkbox" id="noSms" v-model="userForm.noSms">
          <label for="noSms">Не отправлять СМС</label>
        </div>
      </div>

      <div class="title-container">
        <h2>Адрес</h2>
        <address-icon></address-icon>
      </div>
      <div class="container">
        <div>
          <label for="index">Индекс</label>
          <input type="text" id="index" v-model="addressForm.index">
        </div>
        <div>
          <label for="country">Страна</label>
          <input type="text" id="country" v-model="addressForm.country">
        </div>
        <div>
          <label for="region">Область</label>
          <input type="text" id="region" v-model="addressForm.region">
        </div>
        <div>
          <label for="city">Город*</label>
          <input type="text" id="city" v-model="addressForm.city" @blur="$v.addressForm.city.$touch()" :class="{ 'error-input': $v.addressForm.city.$error && $v.addressForm.city.$dirty }">
          <transition name="fade">
          <div v-if="$v.addressForm.city.$error && $v.addressForm.city.$dirty" class="error-message">Город -
            обязательное поле для заполнения
          </div>
          </transition>
        </div>
        <div>
          <label for="street">Улица</label>
          <input type="text" id="street" v-model="addressForm.street">
        </div>
        <div>
          <label for="house">Дом</label>
          <input type="number" id="house" v-model="addressForm.house">
        </div>
      </div>

      <div class="title-container">
        <h2>Паспорт</h2>
        <passport-icon></passport-icon>
      </div>
      <div class="container">
        <div>
          <label for="documentType">Тип документа*</label>
          <select id="documentType" v-model="documentForm.documentType" @blur="$v.documentForm.documentType.$touch()" :class="{ 'error-input': $v.documentForm.documentType.$error && $v.documentForm.documentType.$dirty }">
            <option value="Паспорт">Паспорт</option>
            <option value="Свидетельство о рождении">Свидетельство о рождении</option>
            <option value="Вод. удостоверение">Вод. удостоверение</option>
          </select>
          <transition name="fade">
          <div v-if="$v.documentForm.documentType.$error && $v.documentForm.documentType.$dirty" class="error-message">
            Тип документа - обязательное поле для заполнения
          </div>
          </transition>
        </div>
        <div>
          <label for="series">Серия</label>
          <input type="text" v-model="documentForm.series" id="series">
        </div>
        <div>
          <label for="number">Номер</label>
          <input type="text" v-model="documentForm.number" id="number">
        </div>
        <div>
          <label for="issuedBy">Кем выдан</label>
          <input type="text" v-model="documentForm.issuedBy" id="issuedBy">
        </div>
        <div>
          <label for="issueDate">Дата выдачи*</label>
          <input type="date" v-model="documentForm.issueDate" @blur="$v.documentForm.issueDate.$touch()" :class="{ 'error-input': $v.documentForm.issueDate.$error && $v.documentForm.issueDate.$dirty }" id="issueDate">
          <transition name="fade">
            <div v-if="$v.documentForm.issueDate.$error && $v.documentForm.issueDate.$dirty" class="error-message">Дата
              выдачи - обязательное поле для заполнения
            </div>
          </transition>
        </div>
      </div>
      <div class="button-container">
        <button type="submit">Отправить</button>
      </div>
    </form>
    <div class="dialog-container" v-if="showSuccessDialog">
      <div class="success-dialog">
        <h2>Новый клиент успешно создан!</h2>
        <button @click="closeSuccessDialog" class="dialog-btn">Закрыть</button>
      </div>
    </div>
    <div class="dialog-container" v-if="showErrorDialog">
      <div class="error-dialog">
        <h2>Пожалуйста, корректно заполните все обязательные поля</h2>
          <button @click="closeErrorDialog" class="dialog-btn">Ок</button>
      </div>
    </div>
  </div>
</template>

<script>
import {required, helpers} from "vuelidate/lib/validators";
import clientIcon from "@/icons/client-icon.vue";
import addressIcon from "@/icons/address-icon.vue";
import passportIcon from "@/icons/passport-icon.vue";
import medicalIcon from "@/icons/medical-icon.vue";

export default {
  name: 'App',
  components: {
    clientIcon,
    addressIcon,
    passportIcon,
    medicalIcon
  },
  data() {
    return {
      isSubmitted: false,
      showSuccessDialog: false,
      showErrorDialog: false,
      userForm: {
        surname: '',
        name: '',
        patronymic: '',
        birthdate: '',
        phone: '',
        gender: '',
        clientGroup: [],
        attendingDoctor: '',
        noSms: false
      },
      addressForm: {
        index: '',
        country: '',
        region: '',
        city: '',
        street: '',
        house: ''
      },
      documentForm: {
        documentType: '',
        series: '',
        number: '',
        issuedBy: '',
        issueDate: ''
      }
    };
  },
  validations: {
    userForm: {
      surname: {
        required
      },
      name: {
        required
      },
      birthdate: {
        required
      },
      phone: {
        required,
        isValidPhoneNumber(value) {
          return helpers.regex('phone', /^[7][0-9]{10}$/)(value);
        }
      },
      clientGroup: {
        required
      },
    },
    addressForm: {
      city: {
        required
      }
    },
    documentForm: {
      documentType: {
        required
      },
      issueDate: {
        required
      }
    }
  },
  methods: {
    submitForm() {
      this.isSubmitted = true;
      console.log(this.userForm)
      if (this.$v.$invalid) {
        this.showErrorDialog = true;
        return
      }
      this.showSuccessDialog = true;
    },
    closeSuccessDialog() {
      this.showSuccessDialog = false;
    },
    closeErrorDialog() {
      this.showErrorDialog = false;
    }
  }
};
</script>

<style lang="sass">
$primary: #cb9a74
#app
  font-family: "Ubuntu", sans-serif
  padding-bottom: 50px
  padding-top: 50px

.dialog-container
  position: fixed
  top: 0
  left: 0
  width: 100%
  height: 100%
  background-color: rgba(0, 0, 0, 0.5)
  display: flex
  align-items: center
  justify-content: center
  z-index: 1

.fade-enter-active, .fade-leave-active
  transition: opacity 0.5s, transform 0.5s
  transform-origin: top
  transform: scaleY(1)

.fade-enter, .fade-leave-to
  opacity: 0
  transform: scaleY(0)

.success-dialog,
.error-dialog
  display: flex
  flex-direction: column
  align-items: center
  background-color: #fff
  font-size: 20px
  padding: 30px
  border-radius: 5px
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5)


.success-dialog
  color: darkgreen

.error-dialog
  color: darkred

.dialog-btn
  margin-top: 20px
  background-color: $primary
  color: #fff
  border-radius: 15px
  font-size: 20px
  padding: 10px 16px
  border-style: none
  cursor: pointer
  transition: background-color 0.5s ease

  &:hover
    background-color: #e3bd9b

.main-title-container
  display: flex
  align-items: center
  justify-content: center
  margin-bottom: 30px
  text-align: center
  background-color: $primary
  border-radius: 15px
  padding: 10px 20px
  border: 6px solid #a1ebff

form
  padding: 20px 120px
  border-radius: 15px
  background-color: #5accea
  width: 40%
  margin: 0 auto
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2), 0 6px 6px rgba(0, 0, 0, 0.2)


  h1
    font-size: 48px
    color: #ffffff
    margin: 7px 12px

  label
    font-size: 20px
    color: #5e4436

  input[type="text"],
  input[type="number"],
  input[type="date"],
  input[type="tel"],
  select
    width: calc(100% - 10px)
    padding: 8px
    border-radius: 5px
    margin-bottom: 10px
    font-size: 20px
    border: none
    outline: none

  select[multiple]
    height: auto

  input[type="radio"],
  input[type="checkbox"]
    margin-bottom: 20px
    transform: scale(1.8)
    margin-left: 10px
    margin-right: 8px

  .button-container
    text-align: center
    margin-top: 20px

  button[type="submit"]
    background-color: $primary
    color: #ffffff
    font-weight: bolder
    border: none
    border-radius: 10px
    padding: 20px 30px
    font-size: 26px
    cursor: pointer
    transition: background-color 0.5s ease

    &:hover
      background-color: #e3bd9b

  h2
    font-size: 36px
    color: #ffffff
    text-align: center
    margin: 5px


.error-message
  color: red
  margin-top: 0
  margin-bottom: 15px
  font-size: 16px
  font-weight: bold

.container
  background-color: #a1ebff
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1), 0 6px 6px rgba(0, 0, 0, 0.1)
  padding: 40px
  border-radius: 5px
  margin-bottom: 40px
  margin-top: 20px

.title-container
  display: flex
  align-items: center
  justify-content: center
  border-bottom: 5px solid $primary
  width: 40%
  margin: 0 auto
  transition: width 0.6s ease

  &:hover
    width: 65%

.error-input
  background-color: #fdb5b5


@media screen and (max-width: 1440px)
  form
    width: 60%
    padding: 20px 60px

@media screen and (max-width: 768px)
  #app
    padding: 0
  .success-dialog,
  .error-dialog
    margin: 0 20px
  form
    width: 90%
    padding: 10px 10px
</style>

