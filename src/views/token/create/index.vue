<template>
  <div class="app-container">
    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item label="请输入生成数量">
        <el-input v-model="form.num" type="number" min="1" max="3000" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onCreate">Create</el-button>
      </el-form-item>
    </el-form>
    <el-link type="primary"><h3>格式:地址---私钥</h3></el-link>
    <el-input
      v-model="form.value"
      v-loading="loading"
      type="textarea"
      rows="30"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        num: "",
        value: "",
      },
      loading: "",
    };
  },
  methods: {
    onCreate() {
      var Wallet = require("ethereumjs-wallet");
      this.loading = true;

      // 生成50个钱包地址数量
      for (var i = 0; i < this.form.num; i++) {
        const val = this.form.value;
        const EthWallet = Wallet.default.generate(false);
        const address = EthWallet.getAddressString();
        const privateKey = EthWallet.getPrivateKeyString();
        this.form.value = val + address + "---" + privateKey + "\n";
      }
      this.loading = false;
    },
  },
};
</script>

<style scoped>
.line {
  text-align: center;
}
</style>
