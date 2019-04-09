<template>
  <v-layout row wrap>
    <sub-nav :pid="6" :rules="this.$store.state.adminGroupRules" />
    <v-flex xs12>
      <v-card>
        <v-card-title primary-title>修改账号密码</v-card-title>

        <v-form @submit.prevent="submit">
          <v-container grid-list-xs>
            <v-flex xs6>

              <v-text-field
      
                label="输入密码"
                type="text"
                placeholder="输入密码"
                v-model="postData.password"
                
              ></v-text-field>
              <v-text-field
                label="再次输入密码"
                type="text"
                placeholder="再次输入密码"
                v-model="postData.password_again"
                required
              ></v-text-field>
             
              <v-btn color="blue" type="submit" class="ml-0">提交</v-btn>
            </v-flex>
          </v-container>
        </v-form>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import SubNav from './../../components/SubNav';

export default {
  asyncData({ store, route }) {
    
  },
  data() {
    return {
      postData:{
        password:'',
        password_again:''
      }
    };
  },
  components: {
    SubNav
  },
  computed: {
    
  },
  methods: {
    async submit() {
      let postData = this.postData;
      postData.id = this.$store.state.AUTH.admin.id
    
      console.log(postData);
      // return
      if (!postData.password){
        alert('密码不能为空')
        return
      }
      if(postData.password != postData.password_again){
        alert('两次密码输入不一致')
        return
      }
      let ret = await this.$store.dispatch("adminUpdate", postData);
      console.log("submit ret", ret);
      if (ret.code == 0) {
        this.$router.go(-1);
      }
    }
  }
};
</script>

<style>
</style>
