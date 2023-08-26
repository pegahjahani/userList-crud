<!-- Please remove this file from your project -->
<template>
  <div class="parentForm d-flex justify-content-center algn-items-center col-12">
    <form class="col-8 form">
      <div class="leftForm  col-6">
        <div class="col-5  boxForm">
          <label for="frirstName">firstName : </label>
          <input class="input_form" id="firstName" name="firstName" placeholder="enter your firstName"
            v-model="data.firstName" />
        </div>
        <div class="col-5 boxForm">
          <label for="lastName">lastName : </label>
          <input class="input_form" id="lastName" name="lastName" placeholder="enter your lastName"
            v-model="data.lastName" />
        </div>
        <div class="col-5 boxForm">
          <label for="age">age : </label>
          <input class="input_form" id="age" name="age" placeholder="enter your age" v-model="data.age" />
        </div>
        <div class="col-5 boxForm">
          <label for="job">job : </label>
          <input class="input_form" id="job" name="job" placeholder="enter your job" v-model="data.job" />
        </div>
        <div class="col-5 boxForm">
          <label for="phoneNumber">phoneNumber : </label>
          <input class="input_form" id="phoneNumber" name="phoneNumber" placeholder="enter your phoneNumber"
            v-model="data.phoneNumber" />
        </div>
    
        <div class="col-5  btnBox">
          <button class="btn addBtn" @click.prevent="addUser(data)">submit</button>
          <button class="btn resetBtn" @click.prevent="reset">reset</button>
        </div>
      </div>
      <div class="imageForm col-6">
      <img src="../../static/assets/img/form3.avif" class="img" />
      </div>
    </form>

  </div>
</template>

<script>
export default {
  data() {
    return {
      data: {
        firstName: '', lastName: '', age: '', job: '', phoneNumber: ''
      }
    }
  },
  props: ['addUser','userInfo','reset'],
  watch:{
    userInfo:{
      handler(_info){
        this.data = _info
      },
      deep:true,
      immediate:true
    }
  },
}
</script>
<style scoped>
.parentForm {
  width: 100%;
  height: 500px;
  /* background-color: darkblue; */
  padding: 10px 0 10px 0;
}

.form {
  background-color: white;
  border-radius: 5px !important;
  display: flex;


}

.leftForm {
  display: flex;
  justify-content: center;
  align-items: start;
  flex-direction: column;
  padding-left: 60px;
}

.input_form {
  width: 350px;
  height: 40px;
  border: none;
  border-radius: 3px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
  padding-left: 5px;
}

.input_form::placeholder {
  color: rgba(128, 128, 128, 0.68);
}

.boxForm {
  display: flex;
  flex-direction: column;
}

.btnBox {
  display: flex;
  flex-direction: row;
  justify-content: start;
  align-items: center;
  gap: 10px;
  margin-top: 10px;

}

.addBtn {
  width: 150px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(108, 30, 37);
  color: white;
  border-radius: 5px;
  transition: 1s;
}

.addBtn:hover {
  box-shadow: rgb(108, 30, 37) 0px 1px 3px, rgb(108, 30, 37) 0px 1px 2px;
  color: rgb(108, 30, 37);
  background-color: aliceblue;
  font-weight: bolder;
}

.resetBtn {
  width: 150px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(0, 139, 134);
  color: white;
  border-radius: 5px;
  transition: 1s;
}

.resetBtn:hover {
  box-shadow: rgb(0, 139, 134) 0px 1px 3px, rgb(0, 139, 134) 0px 1px 2px;
  color: rgb(0, 139, 134);
  background-color: aliceblue;
  font-weight: bolder;
}

.imageForm {
  display: flex;
  justify-content: center;
  align-items: center;
}

.img {
  width: 450px;
  height: 450px;
  /* object-fit: cover; */
}

.img>img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}</style>
