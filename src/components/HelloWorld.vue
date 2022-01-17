<template>
  <el-form
    :model="dynamicValidateForm"
    ref="dynamicValidateForm"
    label-width="100px"
    class="demo-dynamic"
  >
    <el-form-item
      prop="email"
      label="邮箱"
      :rules="[
        { required: true, message: '请输入邮箱地址', trigger: 'blur' },
      ]"
    >
      <el-input v-model="dynamicValidateForm.email"></el-input>
    </el-form-item>
    <div v-for="(domain, index) in dynamicValidateForm.domains" :key="index">
      <el-form-item
        :label="'域名' + index"
        :prop="'domains.' + index + '.value'"
        :rules="{
          required: true,
          message: '域名不能为空',
          trigger: 'blur',
        }"
      >
        <el-input v-model="domain.value"></el-input>
      </el-form-item>

      <el-form-item
        label="活动区域"
        :prop="'domains.' + index + '.region'"
        :rules="{
          required: true,
          message: '活动区域',
          trigger: 'change',
        }"
      >
        <el-select placeholder="请选择活动区域" v-model="domain.region">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item
        label="活动区域2"
        :prop="'domains.' + index + '.region1'"
        :rules="{
          required: true,
          message: '活动区域2',
          trigger: 'change',
        }"
      >
        <el-select placeholder="请选择活动区域" v-model="domain.region1">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
        </el-select>
      </el-form-item>
    </div>
    <el-form-item>
      <el-button type="primary" @click="submitForm('dynamicValidateForm')"
        >提交</el-button
      >
      <el-button @click="addDomain">新增</el-button>
      <el-button @click="resetForm('dynamicValidateForm')">重置</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  data() {
    return {
      dynamicValidateForm: {
        domains: [
          {
            value: "",
            region: "",
            region1: "",
          },
        ],
        email: "",
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    removeDomain(item) {
      var index = this.dynamicValidateForm.domains.indexOf(item);
      if (index !== -1) {
        this.dynamicValidateForm.domains.splice(index, 1);
      }
    },
    addDomain() {
      this.dynamicValidateForm.domains.push({
        value: "",
        region: "",
        region1: "",
      });
    },
  },
};
</script>

<style scoped></style>
