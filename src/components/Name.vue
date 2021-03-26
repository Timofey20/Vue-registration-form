<template>
  <form @submit.prevent="check">
    <div
      class="secondName form"
      :class="{ 'form-group--error': $v.formReg.secondName.$error }"
    >
      <label class="form__first" for="secondName"
        >Введите фамилию<span class="necessarily">*</span></label
      ><br />
      <input
        v-model.trim="formReg.secondName"
        @blur="$v.formReg.secondName.$touch()"
        type="text"
        class="form__placeInput is-invalid"
        id="secondName"
      />
      <div
        class="error"
        v-if="$v.formReg.secondName.$dirty && !$v.formReg.secondName.required"
      >
        Обязательное поле
      </div>
      <div
        class="error"
        v-if="$v.formReg.secondName.$dirty && !$v.formReg.secondName.minLength"
      >
        Минимальное число знаков -
        {{ $v.formReg.secondName.$params.minLength.min }}
      </div>
      <div
        class="error"
        v-if="$v.formReg.secondName.$dirty && !$v.formReg.secondName.alpha"
      >
        Только буквы
      </div>
    </div>

    <div>
      <div
        class="name form"
        :class="{ 'form-group--error': $v.formReg.name.$error }"
      >
        <label class="form__first" for="name"
          >Введите имя<span class="necessarily">*</span></label
        ><br />
        <input
          v-model.trim="formReg.name"
          @blur="$v.formReg.name.$touch()"
          type="text"
          class="form__placeInput"
          id="name"
        />
      </div>
      <div
        class="error"
        v-if="$v.formReg.name.$dirty && !$v.formReg.name.required"
      >
        Обязательное поле
      </div>
      <div
        class="error"
        v-if="$v.formReg.name.$dirty && !$v.formReg.name.minLength"
      >
        Минимальное число знаков - {{ $v.formReg.name.$params.minLength.min }}
      </div>
      <div
        class="error"
        v-if="$v.formReg.name.$dirty && !$v.formReg.name.alpha"
      >
        Только буквы
      </div>
    </div>

    <div class="patronymic form">
      <label class="form__first" for="patronymic">Введите отчество</label><br />
      <input
        v-model="formReg.patronymic"
        type="text"
        class="form__placeInput"
        id="patronymic"
      />
    </div>

    <div
      class="birthday form"
      :class="{ 'form-group--error': $v.formReg.year.$error }"
    >
      <label class="form__first" for="day"
        >Введите дату рождения<span class="necessarily">*</span></label
      ><br />
      <input
        v-model.trim="formReg.year"
        @blur="$v.formReg.year.$touch()"
        type="text"
        class="form__placeInput"
        id="year"
      />
      <div
        class="error"
        v-if="$v.formReg.year.$dirty && !$v.formReg.year.required"
      >
        Обязательное поле
      </div>
      <div
        class="error"
        v-if="$v.formReg.year.$dirty && !$v.formReg.year.minLength"
      >
        Минимальное число знаков - {{ $v.formReg.year.$params.minLength.min }}
      </div>
      <div class="error" v-if="$v.formReg.year.$dirty && !$v.formReg.year.date">
        Только цифры и точки
      </div>
    </div>

    <div class="gender form">
      <div class="form_radio">
        <input
          v-model="formReg.gender"
          type="radio"
          class="form__placeInput"
          name="gender"
          id="gender-1"
          value="M"
        />
        <label class="form__first" for="gender-1">Мужчина</label>
      </div>
      <div class="form_radio">
        <input
          v-model="formReg.gender"
          type="radio"
          class="form__placeInput"
          name="gender"
          value="W"
          id="gender-2"
        />
        <label class="form__first" for="gender-2">Женщина</label>
      </div>
    </div>
    <button type="submit" class="btn button-primary">
      Следующий шаг
    </button>
  </form>
</template>

<script>
import { required, minLength, helpers } from "vuelidate/lib/validators";
const alpha = helpers.regex("alpha", /^[a-zA-Zа-яёА-ЯЁ]*$/);
const date = helpers.regex("date", /^[0-9.]*$/);
import "./styleName.scss";
export default {
  data() {
    return {
      formReg: {
        secondName: "",
        name: "",
        year: "",
        patronymic: "",
        gender: "",
      },
    };
  },
  validations: {
    formReg: {
      secondName: {
        required,
        minLength: minLength(2),
        alpha,
      },
      name: {
        required,
        minLength: minLength(2),
        alpha,
      },
      year: {
        required,
        minLength: minLength(10),
        date,
      },
    },
  },
  methods: {
    check() {
      this.$v.formReg.$touch();
      if (!this.$v.formReg.$error) {
        this.$emit("nextStep");
      }
    },
  },
};
</script>
