<template>
  <div class="money">
      <div class="money-form">
        <label for="cost" class="label">Стоимость недвижимости</label>
        <input id="cost" type="text" class="money-form__input" inputmode="numeric"> <span class="money-form__etc"> ₽</span>

        <label for="fee" class="label">Первоначальный взнос</label>
        <input id="fee" type="text" class="money-form__input" inputmode="numeric"> <span class="money-form__etc"> ₽</span>

        <div class="money-form-percent">
          <input name="percent" type="radio" id="10" value="10" class="money-form-percent__radio" v-model="picked">
          <label for="10" class="money-form-percent__label">
            10%</label>

          <input name="percent" type="radio" id="15" value="15" class="money-form-percent__radio" v-model="picked">
          <label for="15" class="money-form-percent__label">
            15%</label>

          <input name="percent" type="radio" id="20" value="20" class="money-form-percent__radio" v-model="picked">
          <label for="20" class="money-form-percent__label">
            20%</label>

          <input name="percent" type="radio" id="25" value="25" class="money-form-percent__radio" v-model="picked">
          <label for="25" class="money-form-percent__label">
            25%</label>

          <input name="percent" type="radio" id="30" value="30" class="money-form-percent__radio" v-model="picked">
          <label for="30" class="money-form-percent__label">
            30%</label>
        </div>
        
        <label for="time" class="label">Срок кредита</label>
        <input id="time" type="text" class="money-form__input" inputmode="numeric"><span class="money-form__etc">лет</span>

        <label for="rate" class="label">Процентная ставка</label>
        <input id="rate" type="text" class="money-form__input" inputmode="numeric"><span class="money-form__etc">%</span>

        <div class="money-form-button">
          <button class="money-form-button__save btn">Save</button>
          <button class="money-form-button__clear btn">Clear</button>
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
  name: "Payment",
}
</script>

