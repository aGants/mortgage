<template>
  <div class="money">
      <div class="money-form">
        <label for="cost" class="label">Стоимость недвижимости</label>
        <input id="cost" type="text" class="money-form__input" inputmode="numeric">

        <label for="fee" class="label">Первоначальный взнос</label>
        <input id="fee" type="text" class="money-form__input" inputmode="numeric">

        <div class="money-form-percent">
          <input name="percent" type="radio" id="10" value="10" v-model="picked" checked>
          <label for="10">10%</label>

          <input name="percent" type="radio" id="15" value="15" v-model="picked">
          <label for="15">15%</label>

          <input name="percent" type="radio" id="20" value="20" v-model="picked">
          <label for="20">20%</label>

          <input name="percent" type="radio" id="25" value="25" v-model="picked">
          <label for="25">25%</label>

          <input name="percent" type="radio" id="30" value="30" v-model="picked">
          <label for="30">30%</label>
        </div>
        
        <label for="time" class="lebel">Срок кредита</label>
        <input id="time" type="text" class="money-form__input" inputmode="numeric">

        <label for="rate" class="label"></label>
        <input id="rate" type="text" class="money-form__input" inputmode="numeric">

        <div class="money-form-buttons">
          <button class="money-form-button__save">Save</button>
          <button class="money-form-button__cleaer">Clear</button>
        </div>

      </div>

      <div class="money-total">
        <span class="label">Ежемесячный платёж</span>
        <span class="money-total__output"> ₽</span>

        <span class="label">Необходимый доход</span>
        <span class="money-total__output"> ₽</span>

        <span class="label">Переплата</span>
        <span class="money-total__output"> ₽</span>

        <span class="label">Тело кредита</span>
        <span class="money-total__output"> ₽</span>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Payment',
}
</script>

