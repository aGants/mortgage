<template>
  <div class="money">
      <div class="money-form">
        <label for="cost" class="label">Стоимость недвижимости</label>
        <money v-bind="money" @input="calculateFee()" v-model="form.cost" id="cost" 
        type="text" pattern="[0-9]" class="money-form__input" inputmode="numeric"></money>
        <span class="money-form__etc"> ₽</span>

        <label for="fee" class="label">Первоначальный взнос</label>
        <money v-bind="money" @input="calculateCost()" v-model="form.fee" id="fee"
        type="text" pattern="[0-9]" class="money-form__input" inputmode="numeric"></money>
        <span class="money-form__etc"> ₽</span>


        <div class="money-form-percent">
          <input @change="calculateFee()" v-model.number="form.percent" name="percent" type="radio" 
          id="10" value="10" class="money-form-percent__radio">
          <label for="10" class="money-form-percent__label">10%</label>

          <input @change="calculateFee()" v-model.number="form.percent" name="percent" type="radio" 
          id="15" value="15" class="money-form-percent__radio">
          <label for="15" class="money-form-percent__label">15%</label>

          <input @change="calculateFee()" v-model.number="form.percent" name="percent" type="radio" 
          id="20" value="20" class="money-form-percent__radio">
          <label for="20" class="money-form-percent__label">20%</label>

          <input @change="calculateFee()" v-model.number="form.percent" name="percent" type="radio" 
          id="25" value="25" class="money-form-percent__radio">
          <label for="25" class="money-form-percent__label">25%</label>

          <input @change="calculateFee()" v-model.number="form.percent" name="percent" type="radio" 
          id="30" value="30" class="money-form-percent__radio">
          <label for="30" class="money-form-percent__label">30%</label>
        </div>
        

        <label for="time" class="label">Срок кредита</label>
        <input v-model.number="form.time" id="time" type="number" class="money-form__input" 
        inputmode="numeric"><span class="money-form__etc">лет</span>

        <label for="rate" class="label">Процентная ставка</label>
        <input v-model.number="form.rate" id="rate" type="number" class="money-form__input" 
        inputmode="numeric"><span class="money-form__etc">%</span>

        <div class="money-form-button">
          <button class="money-form-button__save btn" @click="toSave()">Save</button>
          <button class="money-form-button__clear btn" @click="toClear()">Clear</button>
        </div>

      </div>


      <div class="money-total">
          <p class="label">Ежемесячный платёж
          <span class="money-total__output"> {{ pay | format }} ₽</span>
          </p>
        
          <p class="label">Необходимый доход
          <span class="money-total__output"> {{ income | format  }} ₽</span>
          </p>

          <p class="label">Переплата
          <span class="money-total__output"> {{ overpay | format  }} ₽</span>
          </p>

          <p class="label">Тело кредита
          <span class="money-total__output"> {{ credit | format  }} ₽</span>
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
        money: {
        decimal: ' ',
        thousands: ' ',
        precision: 0,
        masked: false
      }
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
    calculateCost() {
      if (this.form.percent != '') {
        this.form.cost = this.form.fee/this.form.percent*100;
      }
    },

    calculateFee() {
      if (this.form.percent != '') {
          if (this.form.cost == '') {
            this.form.cost = this.form.fee/this.form.percent*100;
          }
          else {
            this.form.fee = this.form.cost*this.form.percent/100;
          }
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
    // C = W - A, где C - тело кредита, W - стоимость недвижимости, A - первоначальный взнос
    credit: function () {
      return this.form.cost - this.form.fee;
    },

    // I - процентная ставка
    division: function () {
      if (this.form.rate === '') {
        return 1
      } else { return this.form.rate/1200 }
    },
    // * P = C * (I / 1200 + (I / 1200) / ((1 + I / 1200) ^ n - 1)), где P - ежемесячный платеж, C - тело кредита,
    // I - процентная ставка, n - срок кредитования (в месяцах)
    pay: function () {
      if (this.form.time === '') {
        return 0 
      } else {
        return (this.credit * 
        (this.division + (this.division / ( ( (1 + this.division)**(this.form.time * 12)) - 1 ) ) ) )
        .toFixed(0); 
      }
    },

    // I = 5 * P / 3, где I - необходимый доход, P - ежемесячный платеж
    income: function () {
      return (5 * (this.pay / 3)).toFixed(0)
    },

    // L = P * n - W + A, где L - переплата, P - ежемесячный платеж, n - срок кредитования (в месяцах),
    //  * W - стоимость недвижимости, A - первоначальный взнос
    overpay: function () {
      return (this.pay * (this.form.time*12)) - this.form.cost + this.form.fee;
    },
  },

  filters: {
    format: val => `${val}`.replace(/(\d)(?=(\d{3})+([^\d]|$))/g, '$1 '),
  }
}
</script>

