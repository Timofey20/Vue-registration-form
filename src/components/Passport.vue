<template>
  <form class="form" @submit.prevent="check_in">
    <div class="form">
      <label class="form__first" for="documents"
        >Тип документа<span class="necessarily">*</span></label
      >
      <form :class="{ 'form-group--error': $v.formReg.documents.$error }">
        <select
          v-model.trim="formReg.documents"
          class="sel documents"
          id="documents"
        >
          <option value="passport">Паспорт</option>
          <option value="birth certificate">Свидетельство о рождении</option>
          <option value="driver's license"> Вод. удостоверение</option>
        </select>
      </form>
      <div
        class="error"
        v-if="$v.formReg.documents.$dirty && !$v.formReg.documents.required"
      >
        Обязательное поле
      </div>
    </div>

    <div class="form">
      <label class="form__first" for="series">Введите серию и номер</label>
      <div class="series__number">
        <input
          v-model.trim="formReg.series"
          type="text"
          class="form__placeInput series"
          id="series"
          placeholder="Серия"
        />
        <input
          v-model.trim="formReg.passportNumber"
          type="text"
          class="form__placeInput passportNumber"
          id="passportNumber"
          placeholder="Номер"
        />
      </div>
    </div>

    <div class="form">
      <label class="form__first" for="who_issue">Кто выдал</label><br />
      <input
        v-model.trim="formReg.who_issue"
        type="text"
        class="form__placeInput"
        id="who_issue"
      />
    </div>

    <div
      class="form"
      :class="{ 'form-group--error': $v.formReg.date_issue.$error }"
    >
      <label class="form__first" for="date_issue"
        >Дата выдачи<span class="necessarily">*</span></label
      ><br />
      <input
        v-model.trim="formReg.date_issue"
        type="text"
        class="form__placeInput"
        id="date_issue"
      />
      <div
        class="error"
        v-if="$v.formReg.date_issue.$dirty && !$v.formReg.date_issue.required"
      >
        Обязательное поле
      </div>
      <div
        class="error"
        v-if="$v.formReg.date_issue.$dirty && !$v.formReg.date_issue.minLength"
      >
        Минимальное число знаков -
        {{ $v.formReg.date_issue.$params.minLength.min }}
      </div>
      <div
        class="error"
        v-if="$v.formReg.date_issue.$dirty && !$v.formReg.date_issue.date"
      >
        Только цифры и точки
      </div>
    </div>

    <div class="buttons">
      <button @click="$emit('backStep')" type="button" class="btn button-back">
        Назад
      </button>
      <button type="submit" class="btn button-head">
        Регистрация
      </button>
    </div>
  </form>
</template>

<script>
import { required, helpers, minLength } from "vuelidate/lib/validators";
const date = helpers.regex("date", /^[0-9.]*$/);
import "./styleName.scss";

export default {
  data() {
    return {
      formReg: {
        documents: "",
        series: "",
        passportNumber: "",
        who_issue: "",
        date_issue: "",
      },
    };
  },
  validations: {
    formReg: {
      documents: {
        required,
      },
      date_issue: {
        required,
        minLength: minLength(10),
        date,
      },
    },
  },
  methods: {
    check_in() {
      this.$v.formReg.$touch();
      if (!this.$v.formReg.$error) {
        alert("Регистрация прошла успешно");
        console.log("Регистрация прошла успешно");
      }
    },
  },
};
</script>
<style scoped>
.form-group--error > select {
  border: 1px solid red !important;
}
</style>
