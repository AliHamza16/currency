<template>
  <div class="currency-box">
    <img :src="flag" :alt="code" class="flag" />
    <div class="title-box">
      <span class="code">{{ code }}</span>
      <span class="title" id="title">{{ titleD }}</span>
    </div>
    <div class="value-box">
      <span class="value">{{ value }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "CurrencyItem",
  props: {
    title: String,
    value: String,
    code: String,
  },
  data() {
    return {
      flag: this.title ? `flags/${this.code}.png` : "default.png",
      hover: "",
      titleD: this.title,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.currency-box {
  display: flex;
  width: 400px;
  background-color: #d4d4d4;
  border-radius: 20px;
  user-select: none;
  transition: 0.3s;
  margin: 20px;
}

.currency-box:hover {
  width: 450px;
}

.currency-box .flag {
  width: 80px;
  height: 80px;
  border-radius: 20px;
}

.currency-box .title-box {
  margin-left: 1.5em;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  font-family: Arial, Helvetica, sans-serif;
}

.currency-box .title-box .code {
  font-weight: bold;
}

.currency-box .title-box .title {
  text-overflow: ellipsis;
  text-align: left;
}

.currency-box .value-box {
  display: flex;
  margin-left: auto;
  margin-right: 1em;
  align-items: center;
  justify-content: center;
}

.currency-box .value-box .value {
  padding: 1em;
  background-color: rebeccapurple;
  border-radius: 10px;
  color: white;
}
</style>
