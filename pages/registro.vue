<template>
    <div class="register-container">
      <div class="register-main">
        <div class="register-section-one section-container">
          <div class="register-max-width max-content-container">
            <div class="register-container-form">
              <div class="register-title">
                <h3 class="register-text">¡Comencemos!</h3>
              </div>
              <form @submit.prevent="ingreso" class="register-form">
                <input
                  id="NameUsu" v-model="name"
                  type="text"
                  required
                  autofocus
                  placeholder="Name"
                  class="register-textinput input"

                />
                <input
                  type="email" id="email" v-model="email"
                  required
                  autofocus
                  placeholder="Email"
                  class="register-textinput1 input"
                />
                <input
                  type="password" id="password" v-model="password"
                  required
                  autofocus
                  placeholder="Password"
                  class="register-textinput2 input"
                />
                <div class="register-max-whidth-bottun">
                  <button class="register-button button">Sign UP</button>
                </div>
              </form>
              <div class="register-container-link">
                <span class="register-text1">¿Ya tienes una cuenta?</span>
                <router-link to="/login" class="register-text2">
                  Iniciar sesión
              </router-link>
              </div>
            </div>
            <div class="register-container-imagen">
              <div class="register-container-img">
                <img
                  alt="image"
                  src="../static/Imagenes/compass-7592447_1280.jpeg"
                  class="register-image"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>

  import axios from 'axios';
  
  export default {
    name: 'Register',
    props: {},
  
    data() {
      return {
        name:'',
        email: '',
        password: '',
      };
    },
    methods: {
      async ingreso() {
        await axios.post('https://backend-helptravel-production.up.railway.app/api/signup', {
          nameUser: this.name,
          email: this.email,
          password: this.password,
        })
          .then((respuesta) => {
            const token = respuesta.data.token;
            localStorage.setItem('token', token);
            this.$router.replace('/envio01');
          })
          .catch(error => {
            this.$swal({
              title: 'ERROR',
              text: '¡ERROR en vista Registro!',
              icon: 'warning',
              confirmButtonColor: 'red',
            });
          });
      },
    },
  };
  </script>
  
  <style scoped>
  .register-container {
    width: 100%;
    display: flex;
    overflow: auto;
    min-height: 100vh;
    align-items: center;
    flex-direction: column;
  }
  .register-main {
    width: 100%;
    height: 751px;
    display: flex;
    padding: var(--dl-space-space-halfunit);
    align-items: flex-start;
    flex-direction: column;
  }
  .register-section-one {
    height: 738px;
    display: flex;
    align-self: center;
    align-items: flex-start;
    padding-top: 0px;
    border-radius: 16px;
    flex-direction: column;
    background-color: #EEEEEE;
  }
  .register-max-width {
    height: 842px;
    display: flex;
    align-self: center;
    align-items: flex-start;
    padding-top: 0px;
    padding-left: 5px;
    padding-right: 2px;
    flex-direction: row;
    padding-bottom: var(--dl-space-space-fiveunits);
    justify-content: center;
  }
  .register-container-form {
    width: 426px;
    display: flex;
    z-index: 100;
    box-shadow: 5px 5px 10px 0px #d4d4d4;
    margin-top: 160px;
    align-items: flex-start;
    margin-left: var(--dl-space-space-unit);
    margin-right: var(--dl-space-space-unit);
    border-radius: 24px;
    flex-direction: column;
    background-color: var(--dl-color-grays-white80);
  }
  .register-title {
    flex: 0 0 auto;
    width: auto;
    display: flex;
    align-self: stretch;
    align-items: flex-start;
    padding-top: 24px;
    padding-left: 24px;
    padding-right: 24px;
    flex-direction: column;
  }
  .register-text {
    font-size: 30px;
    align-self: center;
    font-style: normal;
    text-align: left;
    font-family: "Open Sans";
    font-weight: 700;
    line-height: 1.375;
    margin-bottom: var(--dl-space-space-halfunit);
    background-image: linear-gradient(135deg, rgba(255, 215, 0, 0.9) 0%, rgb(250, 121, 48) 63%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .register-form {
    width: 100%;
    height: 328px;
    display: flex;
    padding: 28px;
    flex-direction: column;
  }
  .register-textinput {
    color: #495057;
    height: auto;
    display: block;
    font-size: 13px;
    appearance: none;
    margin-top: var(--dl-space-space-halfunit);
    transition: 0.3s;
    font-weight: 400;
    line-height: 22,4px;
    padding-top: var(--dl-space-space-halfunit);
    border-color: #afafaf;
    padding-left: 12px;
    border-radius: var(--dl-radius-radius-radius8);
    margin-bottom: var(--dl-space-space-oneandhalfunits);
    padding-right: 12px;
    padding-bottom: var(--dl-space-space-halfunit);
    background-clip: padding-box;
  }
  .register-textinput:focus {
    box-shadow: 0px 0px 10px 0px #fa7930;
    border-color: var(--dl-color-backgrounds-primary);
    border-style: dotted;
  }
  .register-textinput1 {
    color: #495057;
    height: auto;
    display: block;
    font-size: 13px;
    appearance: none;
    margin-top: 0px;
    transition: 0.3s;
    font-weight: 400;
    line-height: 22,4px;
    padding-top: var(--dl-space-space-halfunit);
    border-color: #afafaf;
    padding-left: 12px;
    border-radius: var(--dl-radius-radius-radius8);
    margin-bottom: var(--dl-space-space-oneandhalfunits);
    padding-right: 12px;
    padding-bottom: var(--dl-space-space-halfunit);
    background-clip: padding-box;
  }
  .register-textinput1:focus {
    box-shadow: 0px 0px 10px 0px #fa7930;
    border-color: var(--dl-color-backgrounds-primary);
    border-style: dotted;
  }
  .register-textinput2 {
    color: #495057;
    height: auto;
    display: block;
    font-size: 13px;
    appearance: none;
    transition: 0.3s;
    font-weight: 400;
    line-height: 22,4px;
    padding-top: var(--dl-space-space-halfunit);
    border-color: #afafaf;
    padding-left: 12px;
    border-radius: var(--dl-radius-radius-radius8);
    padding-right: 12px;
    padding-bottom: var(--dl-space-space-halfunit);
    background-clip: padding-box;
  }
  .register-textinput2:focus {
    box-shadow: 0px 0px 10px 0px #fa7930;
    border-color: var(--dl-color-backgrounds-primary);
    border-style: dotted;
  }
  .register-max-whidth-bottun {
    flex: 0 0 auto;
    width: 367px;
    height: auto;
    display: flex;
    align-self: stretch;
    margin-top: var(--dl-space-space-twounits);
    align-items: center;
    justify-content: center;
  }
  .register-button {
    color: var(--dl-color-grays-white100);
    width: 100%;
    height: 43px;
    font-size: 12px;
    font-style: normal;
    text-align: center;
    transition: 0.3s;
    font-family: "Open Sans";
    font-weight: 600;
    border-radius: var(--dl-radius-radius-radius8);
    text-transform: uppercase;
    background-image: linear-gradient(135deg, rgba(255, 215, 0, 0.9) 0%, rgb(250, 121, 48) 63%);
  }
  .register-button:active {
    width: var(--dl-size-size-xxlarge);
  }
  .register-container-link {
    width: 100%;
    height: 65px;
    display: flex;
    margin-top: var(--dl-space-space-halfunit);
    align-items: flex-start;
    padding-left: 4px;
    padding-right: 4px;
    padding-bottom: 24px;
    justify-content: center;
  }
  .register-text1 {
    color: rgb(103, 116, 142);
    font-size: 14px;
    font-style: normal;
    font-family: "Open Sans";
    font-weight: 500;
    margin-bottom: 24px;
  }
  .register-text2 {
    font-size: 14px;
    font-style: normal;
    font-family: "Open Sans";
    font-weight: 500;
    margin-bottom: 24px;
    background-image: linear-gradient(135deg, rgba(255, 215, 0, 0.9) 0%, rgb(250, 121, 48) 63%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .register-container-imagen {
    top: 0px;
    left: 0px;
    right: 0px;
    width: 100%;
    height: 100%;
    margin: auto;
    display: flex;
    z-index: 50;
    position: absolute;
    align-items: flex-end;
    flex-direction: column;
  }
  .register-container-img {
    width: 100%;
    height: 320px;
    display: flex;
    border-radius: var(--dl-radius-radius-radius4);
    flex-direction: column;
    border-bottom-left-radius: 16px;
  }
  .register-image {
    width: 100%;
    height: 320px;
    align-self: center;
    object-fit: cover;
    border-radius: var(--dl-radius-radius-radius4);
    border-bottom-left-radius: 16px;
  }
  </style>
  