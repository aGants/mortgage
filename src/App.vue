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

* {
  box-sizing: border-box;
}

.app {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 50px;
  color: #2c3e50;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.money {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;

  .label {
    display: block;
    margin: $margin;
  }

  &-form {
    &-percent {
      display: flex;
      justify-content: space-between;
      margin: -10px 0 20px;

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
      gap: 10px;
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
        &:active {
          background: #8EDCB9;
        }
      }

      &__clear {
        background: #ddd;
        border: 1px solid #666666;
        &:hover {
          background: #9f9f9f;
        }
        &:active {
          background: #666666;
        }
      }
    }

    &__etc {
      display: block;
      position: relative;
      left: 87%;
      top: -25px;
      padding: auto;
      width: 25px;
      text-align: right;
    }
    
    &__input {
      display: inline-block;
      width: 100%;
      height: 30px;
      padding: 2px 40px 2px 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      &:hover, &:focus, &:active  {
        border: 1px solid #A6A6A6;
        outline: none;
      }
    }

  }

  &-total {
    display: flex;
    justify-content: space-around;
    align-content: center;
    flex-wrap: wrap;
    max-width: 400px;
    height: 150px;
    padding: 0 10px;
    border-radius: 10px;
    background: #f2f2f2;
    .label {
      width: 45%;
      margin-left: 1%;
    }

    &__output {
      display: block;
      font-size: 20px;
    }

  }
}

</style>
