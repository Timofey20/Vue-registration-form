<template>
  <form class="form" @submit.prevent="check">
    <div class="form">
      <label class="form__first" for="index">Введите индекс</label><br />
      <input
        v-model.trim="formReg.index"
        type="text"
        class="form__placeInput"
        id="index"
      />
    </div>

    <div class="form">
      <label class="form__first" for="country">Введите страну</label><br />
      <input
        v-model.trim="formReg.country"
        type="text"
        class="form__placeInput"
        id="country"
      />
    </div>

    <div class="form">
      <label class="form__first" for="region">Введите область</label><br />
      <input
        v-model.trim="formReg.region"
        type="text"
        class="form__placeInput"
        id="region"
      />
    </div>

    <div class="form" :class="{ 'form-group--error': $v.formReg.town.$error }">
      <label class="form__first" for="town"
        >Введите город<span class="necessarily">*</span></label
      ><br />
      <input
        v-model.trim="formReg.town"
        @blur="$v.formReg.town.$touch()"
        type="text"
        class="form__placeInput"
        id="town"
      />
      <div
        class="error"
        v-if="$v.formReg.town.$dirty && !$v.formReg.town.required"
      >
        Обязательное поле
      </div>
      <div
        class="error"
        v-if="$v.formReg.town.$dirty && !$v.formReg.town.minLength"
      >
        Минимальное число знаков -
        {{ $v.formReg.town.$params.minLength.min }}
      </div>
      <div
        class="error"
        v-if="$v.formReg.town.$dirty && !$v.formReg.town.alpha"
      >
        Только буквы
      </div>
    </div>

    <div class="form">
      <label class="form__first" for="street">Введите улицу и дом</label><br />
      <div class="street__town">
        <input
          v-model.trim="formReg.street"
          type="text"
          class="form__placeInput street"
          id="street"
          placeholder="Улица"
        />
        <input
          v-model.trim="formReg.house"
          type="text"
          class="form__placeInput house"
          id="house"
          placeholder="Дом"
        />
      </div>
    </div>
    <div class="buttons">
      <button @click="$emit('backStep')" type="button" class="btn button-back">
        Назад
      </button>
      <button type="submit" class="btn button-head">
        Следующий шаг
      </button>
    </div>
  </form>
</template>

<script>
import { required, minLength, helpers } from "vuelidate/lib/validators";
const alpha = helpers.regex("alpha", /^[a-zA-Zа-яёА-ЯЁ]*$/);
import "./styleName.scss";
export default {
  name: "direction",
  data() {
    return {
      formReg: {
        town: "",
        street: "",
        house: "",
        index: "",
        country: "",
        region: "",
      },
    };
  },
  validations: {
    formReg: {
      town: {
        required,
        minLength: minLength(2),
        alpha,
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
