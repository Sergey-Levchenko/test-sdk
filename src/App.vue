<template>
  <div id="app">
    <section class="info" :class="{active: paymentActive}" @click="paymentActive=!paymentActive">
      <div>
        <div class="info__buying" v-if="paymentActive">
          <h2>You are buying</h2>
          <p>Flight in space /Jupiter Area</p>
          <p>
            <strong>From IO to GANIMED, J29, 2048, G5/42</strong>
          </p>
          <p>Spaceship "Queen of the Sun"</p>
        </div>
        <div class="info__amount">
          <h4 v-if="!paymentActive">Amount to pay</h4>
          <div>42350.00 USD</div>
          <p v-if="paymentActive">Amount to pay without the payment system commission</p>
        </div>
        <div class="info__seller">
          <h2>Seller</h2>
          <p>
            <strong>National Aeronautics and Space</strong>
            <i></i>
          </p>
          <p class="info__corp">
            <strong>Administration (NASA)</strong>
          </p>
          <p>Headquarters 300 E. Street SW, Suite 5R30</p>
          <p>
            <span>Rating:</span> 5
          </p>
          <p>
            <span>Reviews:</span> 308 042
          </p>
        </div>
      </div>
      <div class="info__provid">Provided by Onpay.ru</div>
    </section>
    <section class="main">
      <div class="main__header">
        <h2>Payment method</h2>
        <p>Payment limits</p>
      </div>
      <ul class="method">
        <li
          :class="[`method__item method__item_${i+1}`, {active: paymentMethodActive===i}]"
          v-for="(item, i) in paymentMethods"
          :key="`method__item method__item_${i+1}`"
          @click="paymentMethodActive=i"
        >{{item.name}}</li>
      </ul>
      <ul class="system">
        <li
          v-for="(item, i) in paymentMethods[paymentMethodActive].list"
          :key="item.name+i"
          @click="paymentSystemActive=i"
        >
          <div class="system__image" :class="{active: paymentSystemActive===i}">
            <img :src="require(`./assets/images/${item.image}.png`)" :alt="item.name" />
          </div>
          <p class="system__name">{{item.name}}</p>
          <p class="system__commission">{{item.comission}}</p>
        </li>
      </ul>
      <select class="system-select" id v-model="selectValue">
        <option
          :value="item.name"
          v-for="(item, i) in paymentMethods[0].list"
          :key="`option${i}`"
        >{{item.name}}</option>
      </select>
      <h2>Payment</h2>
      <form action="#" class="payment">
        <div class="payment__item payment__item_amount">
          <label for="amount">Amount with commission</label>
          <input id="amount" type="text" disabled value="43408.75" />
          <span>
            payment system fees
            2.5% (+$1058.75)
          </span>
        </div>
        <div class="payment__item payment__item_email">
          <label for="email">Yandex.Money account</label>
          <input id="email" type="text" />
        </div>
        <div class="payment__item payment__item_phone">
          <label for="phone">Phone</label>
          <input id="phone" type="text" value="+380" />
        </div>
        <div class="payment__item payment__item_message">
          <label for="message">Phone</label>
          <textarea
            id="message"
            placeholder="If you need additional services, please inform the seller about this"
          ></textarea>
        </div>
        <div class="payment__item payment__item_captcha">
          <label for="captcha">Amount with commission</label>
          <input id="captcha" type="text" />
          <div class="payment__captcha"></div>
        </div>
        <p class="payment__terms">
          By clicking "Confirm payment" I realize that the seller is responsible for the quality of the product/services and accept the
          <a
            href="#"
          >terms of the agreement</a>
        </p>
        <div class="payment__submit">Confirm payment</div>
      </form>
    </section>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    paymentActive: false,
    selectValue: "Yandex.Money",
    paymentMethodActive: 0,
    paymentSystemActive: 0,
    paymentMethods: [
      {
        name: "E-money",
        list: [
          {
            name: "Qiwi Wallet",
            comission: "Payment Fees 1.5%",
            image: "qiwi"
          },
          {
            name: "Skrill",
            comission: "Payment Fees 2.5%",
            image: "skrill"
          },
          {
            name: "Payoneer",
            comission: "Payment Fees 5%",
            image: "payoneer"
          },
          {
            name: "Payza",
            comission: "Payment Fees 2.5%",
            image: "payza"
          },
          {
            name: "Yandex.Money",
            comission: "Payment Fees 2.5%",
            image: "yandex"
          },
          {
            name: "PayPal",
            comission: "Payment Fees 0.5%",
            image: "paypal"
          }
        ]
      },
      { name: "Mobile Payments", list: [] },
      { name: "Bank Cards", list: [] },
      { name: "Bank Transfers", list: [] },
      { name: "Terminals", list: [] }
    ]
  })
};
</script>

<style lang="scss">
#app {
  display: flex;
}
.info {
  width: 418px;
  min-height: 100vh;
  background: linear-gradient(180deg, #2931eb 0%, #151cc3 100%);
  color: #ffffff;
  padding: 30px 45px 0 30px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  pointer-events: none;
  &__buying {
    font-size: 1.8rem;
    margin-bottom: 1.5rem;
    line-height: 2.6rem;
    strong {
      font-weight: 700;
    }
  }
  &__amount {
    margin-bottom: 4rem;
    div {
      font-size: 3.4em;
      line-height: 4.9rem;
    }
    p {
      font-size: 1.6rem;
      color: #b4b7f8;
    }
  }
  &__seller {
    font-size: 1.7rem;
    line-height: 2.5rem;
    strong {
      font-weight: 700;
    }
    span {
      color: #b4b7f8;
    }
  }
  &__corp::after {
    content: "";
    display: inline-block;
    width: 22px;
    height: 16px;
    margin-left: 10px;
    margin-bottom: -2px;
    background: url("./assets/images/nlo.png") no-repeat center;
  }
  &__provid {
    font-weight: 700;
    font-size: 1.8rem;
    color: #ffffff;
    margin-bottom: 42px;
  }
}
.main {
  width: 782px;
  min-width: 782px;
  padding: 30px 36px;
  h2 {
    font-size: 2.4rem;
    color: #231f1f;
    margin-bottom: 2rem;
  }
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
    h2 {
      margin-bottom: 0;
    }
    p {
      font-size: 1.6rem;
      color: #5b78b9;
    }
  }
}
.method {
  width: 100%;
  height: 36px;
  border-radius: 5px;
  display: flex;
  overflow: hidden;
  margin-bottom: 14px;
  li {
    background: #edf2fd;
    flex-grow: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #5b78b9;
    font-size: 1.9rem;
    cursor: pointer;
    transition: all 0.3s ease;
    &.active {
      background: #2931eb;
      color: #ffffff;
    }
  }
}
.system {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 35px;
  li {
    margin-right: 10px;
    margin-bottom: 20px;
    text-align: center;
    &:nth-child(4n + 4) {
      margin-right: 0;
    }
  }
  &__image {
    width: 170px;
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 3px solid transparent;
    border-radius: 6px;
    transition: all 0.3s ease;
    background: #edf2fd;
    margin-bottom: 6px;
    &.active {
      border-color: #2931eb;
    }
  }
  &__name {
    font-size: 1.6rem;
  }
  &__commission {
    font-size: 1.5rem;
    font-weight: 400;
  }
}
.system-select {
  width: 100%;
  height: 42px;
  border: 2px solid #b3b3b3;
  box-sizing: border-box;
  border-radius: 6px;
  margin-right: 10px;
  padding: 10px 16px;
  font-size: 1.6rem;
  font-weight: 500;
  color: #231f1f;
  margin-bottom: 30px;
  display: none;
  &:focus {
    outline: none;
    border: 2px solid #2931eb;
  }
}
.payment {
  font-size: 1.6rem;
  line-height: 1.9rem;
  color: #231f1f;
  &__item {
    display: flex;
    align-items: center;
    margin-bottom: 12px;
  }
  label {
    min-width: 204px;
    width: 204px;
    margin-right: 18px;
  }
  input,
  textarea {
    width: 308px;
    height: 42px;
    border: 2px solid #b3b3b3;
    box-sizing: border-box;
    font-weight: 500;
    border-radius: 6px;
    margin-right: 10px;
    padding: 10px 16px;
    color: #231f1f;
    &:disabled {
      background: #efefef;
      border: none;
    }
    &:focus {
      outline: none;
      border: 2px solid #2931eb;
    }
  }
  textarea {
    width: 100%;
    height: 137px;
    resize: none;
  }
  span {
    width: 170px;
    color: #939393;
  }
  &__captcha {
    width: 82px;
    height: 42px;
    border-radius: 6px;
    background: #efefef url("./assets/images/captcha.png") no-repeat center;
  }
  &__terms {
    font-size: 1.5rem;
    margin: 22px 0 22px 222px;
    a {
      color: #2931eb;
      text-decoration-color: rgba(41, 47, 235, 0.3);
    }
  }
  &__submit {
    width: 210px;
    height: 46px;
    background: #2931eb;
    border-radius: 6px;
    margin-left: 222px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 1.8rem;
    color: #ffffff;
  }
}
@media screen and (max-width: 536px) {
  .info {
    pointer-events: all;
    position: fixed;
    min-height: auto;
    height: 59px;
    width: 100%;
    padding: 0 15px;
    background: linear-gradient(180deg, #2f37f4 0%, #1820de 100%);
    box-shadow: 0px 4px 12px rgba(23, 30, 198, 0.35);
    &__buying {
      h2 {
        font-size: 2rem;
      }
      p {
        font-size: 1.6rem;
      }
    }
    & > div {
      height: 100%;
      position: relative;
      &::after {
        content: "";
        display: block;
        position: absolute;
        bottom: 8px;
        left: 50%;
        transform: translateX(-50%);
        width: 28px;
        height: 2px;
        background: #6066f3;
        border-radius: 5px;
      }
    }
    &__buying {
      margin-bottom: 10px;
    }
    &__amount {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 0;
      h4 {
        font-size: 1.6rem;
      }
      div {
        font-size: 1.8rem;
      }
    }
    &__seller,
    &__provid {
      display: none;
    }
    &.active {
      height: 219px;
      width: calc(100vw - 20px);
      border-radius: 6px;
      left: 10px;
      top: 10px;
      padding: 15px;
      & > div::after {
        bottom: -6px;
      }
    }
    &.active .info__amount {
      flex-direction: column;
      align-items: flex-start;
      div {
        font-size: 2.8rem;
        line-height: 2.8rem;
        margin-bottom: 5px;
      }
      p {
      }
    }
  }
  .main {
    width: 100%;
    min-width: 100%;
    padding: 70px 16px 70px;
  }
  .method,
  .system {
    display: none;
  }
  .system-select{
    display: inline-block;
  }
  .payment {
    &__item {
      flex-wrap: wrap;
      label {
        width: 100%;
        margin-bottom: 10px;
      }
      input,
      textarea {
        width: 100%;
      }
      &_captcha {
        input {
          width: 66%;
          margin-right: 4%;
        }
      }
      &__captcha {
        width: 40%;
      }
    }
    &__terms {
      margin-left: 0;
    }
    &__submit {
      margin: 0;
      position: fixed;
      bottom: 16px;
      width: calc(100% - 32px);
      left: 50%;
      transform: translateX(-50%);
    }
  }
}
</style>
