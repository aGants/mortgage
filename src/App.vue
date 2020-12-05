<template>
  <div class="app">
    <Payment />
  </div>
</template>

<script>
import Payment from './components/Payment.vue'

export default {
  name: 'App',
  components: {
    Payment
  }
}
</script>

<style lang="scss">

$margin: 10px 0;

.app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.money {
  display: flex;
  justify-content: space-between;
  gap: 50px;

  .label {
    display: block;
    margin: $margin;
    
  }

  &-form {
    width: 300px;
    &-percent {
      display: flex;
      justify-content: space-between;
      margin: $margin;

      &__radio {
        display: none;
      }
      
      &__radio[type=radio]:checked + &__label {
        color: #fff;
        border-color: #1a73e8;
        background: #1a73e8;
      }

      &__label {
        display: inline-block;
        min-width: 25px;
        padding: 5px 5px;
        text-align: center;
        background: #fbfbfb;
        border: 1px solid #ddd;
        border-radius: 8px;
        user-select: none;
        cursor: pointer;
        &:focus, &:active {
            outline: none;
        }
        &:hover { border-color: #1a73e8; }
      }
    }

    &-button {
      display: flex;
      justify-content: space-between;
      margin: $margin;

      .btn {
        width: 140px;
        padding: 10px;
        border-radius: 5px;
        cursor: pointer;
        &:active, &:focus {
          outline: none;
          user-select: none;
        }
      } 

      &__save {
        color: #fff;
        background: #42b983;
        border: none;
        &:hover {
          background: #72DCAC
        }
        &:focus, &:active {
          background: #8EDCB9;
        }
      }

      &__clear {
        background: #ddd;
        border: 1px solid #666666;
        &:hover {
          background: #9f9f9f;
        }
        &:focus, &:active {
          background: #666666;
        }
      }
    }
    
    &__input {
      width: 100%;
      height: 25px;
      padding: 2px 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      &:hover, &:focus, &:active  {
        border: 1px solid #A6A6A6;
        outline: none;
      }
    }

  }

  &-total {

    background: #f2f2f2;
  }
}

</style>
