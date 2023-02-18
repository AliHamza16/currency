<template>
  <CurrencyItem
    v-for="currency in currency_rates"
    :code="currency[0]"
    :title="titles[currency[0]]"
    :value="currency[1]"
    v-bind:key="currency[0]"
  />
</template>

<script>
import CurrencyItem from "./components/Currency.vue";

export default {
  name: "App",
  components: {
    CurrencyItem,
  },
  data() {
    return {
      currency_rates: null,
      titles: {
        USD: "ABD Doları",
        EUR: "Euro",
        GBP: "İngiliz Sterlini",
        CHF: "İsviçre Frangı",
        CAD: "Kanada Doları",
        RUB: "Rus Rublesi",
        AED: "Birleşik Arap Emirlikleri Dirhemi",
        AUD: "Avustralya Doları",
        DKK: "Danimarka Kronu",
        SEK: "İsveç Kronu",
        NOK: "Norveç Kronu",
        JPY: "Japon Yeni",
        KWD: "Kuveyt Dinarı",
        ZAR: "Güney Afrika Randı",
        BHD: "Bahreyn Dinarı",
        LYD: "Libya Dinarı",
        SAR: "Suudi Arabistan Riyali",
        IQD: "Irak Dinarı",
        ILS: "Yeni İsrail Şekeli",
        IRR: "İran Riyali",
        INR: "Hindistan Rupisi",
        MXN: "Meksika Pesosu",
        HUF: "Macar Forinti",
        NZD: "Yeni Zelanda Doları",
        BRL: "Brezilya Reali",
        IDR: "Endonezya Rupiahı",
        CSK: "Çek Korunası",
        PLN: "Polonya Zlotisi",
        RON: "Rumen Leyi",
        CNY: "Yuan Renminbisi",
        ARS: "Arjantin Pesosu",
        ALL: "Arnavut Leki",
        AZN: "Azerbaycan Manatı",
        BAM: "Bosna-Hersek Markı",
        CLP: "Şili Pesosu",
        COP: "Kolombiya Pesosu",
        CRC: "Kosta Rika Colonu",
        DZD: "Cezayir Dinarı",
        EGP: "Mısır Lirası",
        HKD: "Hong Kong Doları",
      },
    };
  },
  mounted() {
    fetch("https://finans.truncgil.com/v3/today.json")
      .then((response) => response.json())
      .then((data) => {
        this.currency_rates = data;
        delete this.currency_rates.Update_Date;
        Object.keys(this.currency_rates).map((key) => {
          if (this.currency_rates[key].Type !== "Currency" || !this.currency_rates[key].Buying) {
            delete this.currency_rates[key];
          }
          return 0;
        });
        this.currency_rates = Object.keys(this.currency_rates).map((key) => [
          `${key}`,
          this.currency_rates[key].Selling,
        ]);
      });
    setInterval(() => {
      fetch("https://finans.truncgil.com/v3/today.json")
        .then((response) => response.json())
        .then((data) => {
          this.currency_rates = data;
          delete this.currency_rates.Update_Date;
          Object.keys(this.currency_rates).map((key) => {
            if (this.currency_rates[key].Type !== "Currency" || !this.currency_rates[key].Buying) {
              delete this.currency_rates[key];
            }
            return 0;
          });
          this.currency_rates = Object.keys(this.currency_rates).map((key) => [
            `${key}`,
            this.currency_rates[key].Selling,
          ]);
        });
    }, 100000);
  },
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
}
</style>
