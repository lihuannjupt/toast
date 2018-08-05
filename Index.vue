<template lang="html">
  <div  v-show="visible">
    <div class="dj-toast" :style="width">
      <div class="dj-toast-con" v-if="type === 'normal'">
        <p>{{msg}}</p>
      </div>

      <div class="dj-toast-con" v-if="type === 'suc'">
        <span class="dj-toast-icon dj-toast-icon-ok"></span>
        <p>{{msg}}</p>
      </div>

      <div class="dj-toast-con" v-if="type === 'err'">
        <span class="dj-toast-icon dj-toast-icon-err"></span>
        <p>{{msg}}</p>
      </div>

      <div class="dj-toast-con" v-if="type === 'load'">
        <div class="dj-toast-icon1  dj-toast-icon-load">
          <div class='dj-toast-icon-circle'></div>
        </div>
        <p>{{msg}}</p>
      </div>
    </div>
  </div>
</template>

<script>
/**
 * type: normal, suc, err
 */
export default {
  name: "Toast",
  props: {
    msg: {
      type: String,
      default: "hello world"
    },
    type: {
      type: String,
      default: "normal"
    },
    time: {
      type: String
    },
    value:{
      type:Boolean,
      default: 'false'
    }
  },
  data() {
    return {
   
      isShow: true,
      visible: this.value
    
    };
  },
  watch: {
      value (val) {
        this.visible = val
      },
      visible () {
        if(this.visible){
          window.setTimeout(() => {
            if (this.visible) {
              this.visible = false;
              this.$emit('input', false);
              this.$emit('function1');
            }
          }, this.time)
        }
      }
  },
 
  computed: {
    width() {
      if (this.msg && this.msg.length > 6) {
        this.twidth = 195;
        return "width: 195px";
      } else {
        return "width: 130px";
      }
    }
  },
  methods: {
   
  }
};
</script>

<style lang="scss" scoped>
.dj-toast {
  position: fixed;
  top: 50%;
  left: 50%;
  color: #fff;
  transform: translate(-50%, -50%);
  z-index: 1000;
}
@-webkit-keyframes scaleUp {
  0% {
    transform: scale3d(0.6, 0.6, 1);
  }
  100% {
    transform: scale3d(1, 1, 1);
  }
}

@keyframes scaleUp {
  0% {
    transform: scale3d(0.6, 0.6, 1);
    opacity: 0;
  }
  100% {
    transform: scale3d(1, 1, 1);
    opacity: 1;
  }
}

@-webkit-keyframes scaleShock {
  0% {
    transform: scale3d(0.4, 0.4, 1);
  }
  60% {
    transform: scale3d(1.07, 1.07, 1);
  }
  80% {
    transform: scale3d(0.97, 0.97, 1);
  }
  100% {
    transform: scale3d(1, 1, 1);
  }
}

@keyframes scaleShock {
  0% {
    transform: scale3d(0.4, 0.4, 1);
  }
  60% {
    transform: scale3d(1.07, 1.07, 1);
  }
  80% {
    transform: scale3d(0.97, 0.97, 1);
  }
  100% {
    transform: scale3d(1, 1, 1);
  }
}
@keyframes load {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
@-webkit-keyframes load {
  from {
    -webkit-transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(360deg);
  }
}
.dj-toast-con {
  font-size: 15px;
  line-height: 15px;
  padding: 12px;
  text-align: center;
  background: rgba(0, 0, 0, 0.75);
  border-radius: 2px;
  animation: scaleUp 0.1s;

  p {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    font-size: 15px;
    line-height: 25px;
    white-space: wrap;
    overflow: hidden;
    margin-top: 8px;
    margin-bottom: 0;
    &:nth-of-type(1) {
      margin-top: 0;
    }
  }

  .dj-toast-icon1 {
    width: 23px;
    height: 23px;
    display: inline-block;
    margin-top: 7px;
    margin-left: 7px;
    margin-bottom: 3px;
    animation: scaleShock 0.4s;
    text-align: center;
  }
  .dj-toast-icon {
    width: 25px;
    height: 25px;
    display: inline-block;
    margin-top: 3px;
    margin-bottom: 6px;
    animation: scaleShock 0.4s;
    text-align: center;
  }
  .dj-toast-icon-circle {
    background-image: url("data:image/png;base64,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");
    background-size: 23px 23px;
    width: 23px;
    height: 23px;
    position: absolute;
    left: -6px;
    top: -5px;
    animation: load 1s linear infinite;
    -webkit-animation: load 1s linear infinite;
  }
  .dj-toast-icon-load {
    background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAAEEfUpiAAAAAXNSR0IArs4c6QAAA7lJREFUWAm9l0tIFVEYx/VaWWZlJT0MjTKIyLAIbNEyiBYF4TZahD0WEZHQpgh6bVu1kcCIAgkXZS0qCCoyalEQPRdmhhE9DJPQFB/d2+8/95y5Z+7M3K6affCf7/2dOd/MnHOmoABKpVId4pFUKCsR4klwUMoT4JMCZDziCVwSKI3wXmuQNwnuAo8KdfW9Vkj7UnOt7vKElEIIVk/gGteJ3qQxzoE3IJLsRMLjZip781hH+k+3vC/jKFFtGSz3nQi6yVFzk7IP6mKJhBorh7JxNvgVJUCb0sy7nrJydOf8ugVFXqMyekB6x70lNfYuWy6LVwbCcX50ApT0GjwKBOVSTPJmN0Y2V89bJm+pKVgSl4RfDeoP+DG8MImzAw6j4FsNNNWFJi59h1aB1zmyKz5EGXQNRm5Tl4ciHPmYThNUqXnoS4h+E6PmkbFV85y7MioSxQ6DPhBFrRiXBRKyFQKagKb0GEzL9sfqBFcAS3cQ9hklvyIEj5mEr3YU9GPggtXjuB1BL8QwTVniBM5BnuHoAZHixcQPe0aUgYAXBZuoPNtudXzXrBziODvAy5DDMeD/DrxVyzF7I+uN6w4YHQXfTKlwUa2/IKBUy4LvAXNb7uT4Iu4zKLXwTmP0iqnaUSA6D/R2ngDfgEu/UPQR9TvGCiUfN4bbcPs1OjGpzyivXIOVvbuwClz7yHjoqQr4PUAOd9QbIvbSLI9bIDYywtGCbUR2NawPXiZlHNTDk1qs+ATCfHjoTcxRrN0mB2K4kxXgZkwXP2E/EEiIUwgsBy0g11N5jr8irsaE7RS9AbLpklsQZynoMkHbXd+kZAqWmaKWjSBsiSqKfbcJuhrln7CNopqZFoO1cUXw6c3rBKK9cXG57OTtCfkxrgftwC6yUTF60eymczYUkKeBGvdAa57h3tK3gYRuIOoB1Xknm0BydNZT91TLkruDBEsSMQs020j4MxCfEEz3NXKqwHWg804NGAaW6kLrF54dZF8B80yVy/AGPv4xo3uMuAUI+hR1U1pVFhlZp+laUAXeg3rwG7SBVcCl9CGWYmqNzgQuaW+YDg4B+9K5/mxZ+4X+CvaDreAk+ALiaABHQvuJTmyjTlQvsjYofYZTSd4aopm/pSeBnxC3R1Mgj1JzI/jAYx3QdqTN4H/RfQZqABc1uDcoHWicyj5H1Na/R1Fgxhi2AXs8jMj5JyYdctT6eCJgJbgFkmCypBpa8XbGj5jnOYYipRTRMVU/E8UG+pHX2jAEdCr5wXMN/Kxi+yv9AU+OUbLmDOlWAAAAAElFTkSuQmCC");
    background-size: 12px 12px;
    margin-right: 7px;
    float: left;
    position: relative;
    width: 12px;
    height: 12px;
    // animation: none;
  }
  .dj-toast-icon-ok {
    background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAC4AAAAuCAMAAABgZ9sFAAAAn1BMVEUAAAD///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////8Kd3m4AAAANHRSTlMAEAn53AcTzlD8SwPvf3LZylsq54z24bqzRxvTwZgvIRe3nmPEvjLQcWpnOKuRdGFUP3d17U7ngQAAAhVJREFUSMeVltmaojAQhRMSCJuAsou7trY6vc2c93+2+UJUJCjYdUfyk9ReIbpQO8lDnzE/XCe2RXrFHK8d3ImTj82nsBFkAJuN7IllmnRij3IGxMGTH0oOHI6t++k2ArLy0dFzQLjddfcAzA19dRUhDbxHl3pBip22s+Tgi2c2Lfi4vTDNEK16HKbpLRBRMiTHf0TJHNwapL+AkTIebD9Ijx0o3uAIBulvSTMZgXcIb4h2maRdaXaMcoguJe1810pBDNE/qaSV89fYDtBnSV8o6rABl+99SR/Vh41ZP72Q9M13CUa99CQG0DAF7D56eUcb55KEmNyl2lKnM0knl4sQEh9NutAqXrQzlUv647oNnwDmLTHfAP/nvmZCSW9uhQLnHn8HgLQxxapq2rulPVhLmQ8AcE7XuwUA/PGa3+G3Tf2Lxg80AoBC3X01VXPklyOZuUeIsQOAdUPLiBZ6mNy01sCUZgNvrY4xQtJJgrNfczkA7Fo0mcHuptgkgxK93Clz6IMEnlaKFlqmbpE/LA9aW1npzUFgLGMZw9X7ZQGEK71cERsqmJVe2t6GT/WlAwJ1Fscn0aXTpgJwg7zclvasUXkz2PQsjs3rLZVGEEa7YVs9Z0fIpr8YB+BaVa4E2JNh85lCrF4eZZUaZd0NDoiT1VL6JABePhvD8WUMUzWGZ/UYNnqGfD485PUnRKGeEEVid4LxH/NkR/uqs14NAAAAAElFTkSuQmCC");
    background-size: 100% 100%;
  }

  .dj-toast-icon-err {
    background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAC4AAAAuCAMAAABgZ9sFAAAAflBMVEUAAAD////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////vroaSAAAAKXRSTlMA+tzPCAZyEowPTxZLyrnm2X9mMAPutVvB8ZtI7ODSUSsqIRz0lZHAXFQ9rloAAAGGSURBVEjHlZbZkoIwEEU7xEDIyL4q7uvc///BwcKaIEEI58kqTjUNpm9DQ3wlw7hgrIhDqXyaRFQlQw8WVuKrvHIjgNXJ8eQJ4Z2OSc2AyF2N240D8NSjHl7KAacZK30H+JoM1gfgbtzgJ8DNzWmE3L2B/9AHFwdORl/I2osX6nHdI+gXMG+9v/b65ggmX7EfgOv+t3A+a6Pls76D7f/Dg2U0rVPGsH634sClOZ1cOKv3D57P6znviooIDc3r1CB6la/AyUYnjoqIQqR2eoqQyGfMt9I7U6EmO51qKJJIbPUEkkooW12hpBhnW/2MmDbwbHUPOwKErS7AFuoLm1n4qPpFzqNQ6r9pngRSH4J5aih9xGZpTU8f4FlShOPjIR7F5iHM8fh9TXaEYTRKtMhhWHbDRy4Og9HeoWUzGO0DXB0cE7oODiOWjGbMWDJDT8iieAgz9JZHqn1gL18HugAHs1g2uv+t3SrTFywWpbmGn3oNPwdr2FzyodWS13hKlt0nRCmVMfV/Jf4ycDaOpHkAAAAASUVORK5CYII=");
    background-size: 100% 100%;
  }
}
</style>
