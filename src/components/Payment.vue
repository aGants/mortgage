<template>
  <div class="money">
      <div class="money-form">
        <label for="cost" class="label">Стоимость недвижимости</label>
        <input @input="calculateFee()" v-model="form.cost" id="cost" type="text" class="money-form__input" inputmode="numeric"> <span class="money-form__etc"> ₽</span>

        <label for="fee" class="label">Первоначальный взнос</label>
        <input @input="calculateCost()" v-model="form.fee" id="fee" type="text" class="money-form__input" inputmode="numeric"> <span class="money-form__etc"> ₽</span>

        <div class="money-form-percent">
          <input @change="calculateFee()" v-model="form.percent" name="percent" type="radio" id="10" value="10" class="money-form-percent__radio">
          <label for="10" class="money-form-percent__label">
            10%</label>

          <input @change="calculateFee()" v-model="form.percent" name="percent" type="radio" id="15" value="15" class="money-form-percent__radio">
          <label for="15" class="money-form-percent__label">
            15%</label>

          <input @change="calculateFee()" v-model="form.percent" name="percent" type="radio" id="20" value="20" class="money-form-percent__radio">
          <label for="20" class="money-form-percent__label">
            20%</label>

          <input @change="calculateFee()" v-model="form.percent" name="percent" type="radio" id="25" value="25" class="money-form-percent__radio">
          <label for="25" class="money-form-percent__label">
            25%</label>

          <input @change="calculateFee()" v-model="form.percent" name="percent" type="radio" id="30" value="30" class="money-form-percent__radio">
          <label for="30" class="money-form-percent__label">
            30%</label>
        </div>
        
        <label for="time" class="label">Срок кредита</label>
        <input v-model="form.time" id="time" type="text" class="money-form__input" inputmode="numeric"><span class="money-form__etc">лет</span>

        <label for="rate" class="label">Процентная ставка</label>
        <input v-model="form.rate" id="rate" type="text" class="money-form__input" inputmode="numeric"><span class="money-form__etc">%</span>

        <div class="money-form-button">
          <button class="money-form-button__save btn" @click="toSave()">Save</button>
          <button class="money-form-button__clear btn" @click="toClear()">Clear</button>
        </div>

      </div>

      <div class="money-total">
          <p class="label">Ежемесячный платёж
          <span class="money-total__output"> {{ pay }} ₽</span>
          </p>
        
          <p class="label">Необходимый доход
          <span class="money-total__output"> {{ income }} ₽</span>
          </p>

          <p class="label">Переплата
          <span class="money-total__output"> {{ overpay }} ₽</span>
          </p>

          <p class="label">Тело кредита
          <span class="money-total__output"> {{ credit }} ₽</span>
          </p>
      </div>
  </div>
</template>

<script>
export default {
  name: "Payment",
  data() {
    return {
      form: {
        cost: '',
        percent: '',
        fee: '',
        time: '',
        rate: ''
        },
    }
  },
  mounted() {
    if (localStorage.cost) {
      this.form.cost = localStorage.cost;
    }
    if (localStorage.percent) {
      this.form.percent = localStorage.percent;
    }
    if (localStorage.fee) {
      this.form.fee = localStorage.fee;
    }
    if (localStorage.time) {
      this.form.time = localStorage.time;
    }
    if (localStorage.rate) {
      this.form.rate = localStorage.rate;
    }
  },
  methods: {
    calculateFee() {
      if (this.form.percent != '') {
        this.form.fee = this.form.cost*this.form.percent/100;
      }
    },

     calculateCost() {
      if (this.form.percent != '') {
        this.form.cost = this.form.fee/this.form.percent*100;
      }
    },
    toClear() {
      this.form.cost = this.form.percent = this.form.fee = this.form.time = this.form.rate = ''
    },
    toSave() {
      localStorage.cost = this.form.cost;
      localStorage.percent = this.form.percent;
      localStorage.fee = this.form.fee;
      localStorage.time = this.form.time;
      localStorage.rate = this.form.rate;
    }
  },
  computed: {
    credit: function () {
      return this.form.cost - this.form.fee;
    },
    division: function () {
      return this.form.rate/1200
    },
    pay: function () {
      return (this.credit * (this.division + (this.division/( ( (1 + this.division)**(this.form.time * 12)) - 1 ) ) ) ).toFixed(0); 
    },
    income: function () {
      return (5 * (this.pay / 3)).toFixed(0)
    },
    overpay: function () {
      return (this.pay * (this.form.time*12) - this.form.cost + this.form.fee)
    }
  }
}
</script>

