<template>
  <form @submit.prevent="check">
    <div
      class="form"
      :class="{ 'form-group--error': $v.formReg.number.$error }"
    >
      <label class="form__first" for="number"
        >Введите номер телефона<span class="necessarily">*</span></label
      ><br />
      <input
        v-model.trim="formReg.number"
        :class="{ 'form-group--error': $v.formReg.number.$error }"
        @blur="$v.formReg.number.$touch()"
        type="text"
        class="form__placeInput"
        id="number"
      />
      <div
        class="error"
        v-if="$v.formReg.number.$dirty && !$v.formReg.number.required"
      >
        Обязательное поле
      </div>
      <div
        class="error"
        v-if="$v.formReg.number.$dirty && !$v.formReg.number.minLength"
      >
        Минимальное число знаков - {{ $v.formReg.number.$params.minLength.min }}
      </div>
      <div
        class="error"
        v-if="$v.formReg.number.$dirty && !$v.formReg.number.maxLength"
      >
        Максимальное число знаков -
        {{ $v.formReg.number.$params.maxLength.max }}
      </div>
      <div
        class="error"
        v-if="$v.formReg.number.$dirty && !$v.formReg.number.numeric"
      >
        Только цифры
      </div>
      <div
        class="error"
        v-if="$v.formReg.number.$dirty && !$v.formReg.number.first_Number"
      >
        Первая цифра должна быть 7
      </div>
    </div>

    <div class="form">
      <label class="form__first" for="client"
        >Группа клиентов<span class="necessarily">*</span></label
      ><br />
      <form :class="{ 'form-group--error': $v.formReg.client.$error }">
        <select
          v-model.trim="formReg.client"
          @blur="$v.formReg.client.$touch()"
          class="sel"
          id="client"
          multiple
          size="3"
        >
          <option
            v-for="(client, index) in formReg.client_choose"
            :key="index"
            :value="client.value"
            >{{ client.value }}</option
          >
        </select>
      </form>
    </div>
    <div
      class="error"
      v-if="$v.formReg.client.$dirty && !$v.formReg.client.required"
    >
      Обязательное поле
    </div>

    <div class="form">
      <label class="form__first" for="doctor">Лечащий врач</label><br />
      <form>
        <select v-model="formReg.doctor" class="sel doctor" id="doctor">
          <option value="Иванов">Иванов</option>
          <option value="Захаров">Захаров</option>
          <option value="Чернышева">Чернышева</option>
        </select>
      </form>
    </div>

    <div class="form">
      <input v-model="formReg.sms" type="checkbox" value="SMS" id="sms" />
      <label class="form__first" for="sms">Не отправлять СМС</label>
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
import {
  required,
  minLength,
  maxLength,
  numeric,
} from "vuelidate/lib/validators";
const first_Number = (value) => {
  if (value.length == 0) {
    return true;
  }
  return value[0] == "7";
};
import "./styleName.scss";
export default {
  name: "client",
  data() {
    return {
      formReg: {
        number: "",
        client: [],
        client_choose: [
          {
            value: "VIP",
          },
          {
            value: "Проблемные",
          },
          {
            value: "ОМС",
          },
        ],
        doctor: "Иванов",
        sms: false,
      },
    };
  },
  validations: {
    formReg: {
      number: {
        required,
        minLength: minLength(11),
        maxLength: maxLength(11),
        numeric,
        first_Number,
      },
      client: {
        required,
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
<style scoped>
.form-group--error > select {
  border: 1px solid red !important;
}
</style>
