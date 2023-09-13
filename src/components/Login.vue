<template>
  <v-card>
    <v-card-title>เข้าสู่ระบบ</v-card-title>
    <v-card-text>
  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="name"
      :counter="20"
      :rules="nameRules"
      label="ชื่อผู้ใช้งาน"
      required
      outlined
    ></v-text-field>

    <v-text-field
      v-model="password"
      :rules="passwordRules"
      label="รหัสผ่าน"
      required
      outlined
    ></v-text-field>

    <v-btn
      :disabled="!valid"
      color="success"
      @click="Login"
      block
    >
      เข้าสู่ระบบ
    </v-btn>
  </v-form>
</v-card-text>
</v-card>
</template>

<script>

export default {
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'กรุณากรอกชื่อใช้งาน',
        v => (v && v.length <= 10) || 'มึงอย่ากรอกเกิน 20 นะสัสหมา',
      ],
      password: '',
      passwordRules: [
        v => !!v || 'กรุณาใส่รหัสผ่าน',
      ],
      
    }),

    methods: {
      Login(){
      if (this.$refs.form.validate(true)){
        localStorage.setItem('username',this.name)
      this.$EventBus.$emit('getUsername')
        this.$router.push('/')
        
      }
        else{
          alert('ไม่ผ่าน')

        }
      

      },
      validate () {
        this.$refs.form.validate()
      },
      reset () {
        this.$refs.form.reset()
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
    },
  }
    


</script>

<style>

</style>