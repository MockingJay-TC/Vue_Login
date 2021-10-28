<template>
  <section class="container-fluid">
    <div class="row min-vh-100 justify-content-center align-items-center">
      <div class="col-lg-4">
        <div class="login__panel bg-white text-start">
          <div
            class="d-flex justify-content-between alert alert-primary"
            role="alert"
            :style="{ opacity: isAlertShow ? 1 : 0 }"
          >
            <p class="m-auto">
              Login Successfully. <small>Waiting for redirect.</small>
            </p>
            <moon-loader
              :loading="!isLoading"
              color="black"
              size="30px"
              v-bind:style="{
                width: '3px',
                margin: 'auto',
              }"
            ></moon-loader>
          </div>
          <h1 class="display-3 font-weight-bold">Login</h1>
          <p class="font-weight-bold">Welcome back</p>
          <br />
          <form v-on:submit.prevent action="">
            <div class="form-group mb-3">
              <div v-if="!isValid" class="alert alert-danger" role="alert">
                Email is Empty
              </div>
              <label for="email" class="input-label"> Email</label>
              <input
                type="email"
                class="form-control"
                placeholder="Email"
                v-model.trim="email"
              />
            </div>
            <div class="form-group mb-3">
              <div v-if="!isValid" class="alert alert-danger" role="alert">
                Password is Empty
              </div>
              <label for="password" class="input-label"> Password</label>
              <input
                type="password"
                class="form-control"
                placeholder="Password"
                v-model.trim="password"
              />
            </div>
            <div class="form-group mb-3 d-flex justify-content-center">
              <button
                v-if="!isLoading"
                class="btn btn-primary w-25"
                v-on:click="login"
                v-bind:disabled="!formIsValid"
              >
                Login
              </button>
              <button
                v-if="isLoading"
                disabled
                class="btn btn-primary w-25 text-middle"
              >
                <moon-loader
                  class="d-flex justify-content-center"
                  color="black"
                  size="30px"
                  v-bind:style="{
                    'font-weight': 'bold',
                    width: '3px',
                    margin: 'auto',
                  }"
                ></moon-loader>
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import MoonLoader from "vue-spinner/src/MoonLoader.vue";
export default {
  components: {
    MoonLoader: MoonLoader,
  },
  data() {
    return {
      isLoading: false,
      isAlertShow: false,
      email: "",
      password: "",
      isValid: true,
    };
  },
  methods: {
    login: function () {
      this.isLoading = true;
      if (this.formIsValid()) {
        console.log(this.password);
        console.log(this.email);
        this.isValid = true;
        console.log("nice");
      } else {
        this.isValid = false;
        console.log("failed");
      }
      setTimeout(() => {
        this.isLoading = false;
        this.isAlertShow = true;
        setTimeout(() => {
          this.isAlertShow = false;
        }, 1000);
      }, 1000);
    },
    formIsValid: function () {
      if (this.email === "" && this.password === "") {
        return false;
      }
      return true;
    },
  },
};
</script>
<style lang="scss" scoped>
.login__panel {
  .alert {
    &.alert-primary {
      opacity: 0;
      background-color: #007bffa9;
      color: #fff;
      border: none;
      font-size: 18px;
    }
    &.alert-danger {
      border: none;
      font-size: 14px;
      padding: 8px;
    }
    .moon-loader {
      position: absolute;
      top: 0px;
      left: 0px;
    }
  }
}
</style>
