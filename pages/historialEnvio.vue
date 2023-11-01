<template>
    <div class="envio01-container">
        <div class="envio01-max-width">
            <div class="envio01-container-sidelbar">
                <app-sidelbar></app-sidelbar>
                <router-view />
            </div>
            <div class="envio01-menu-container">
                <app-navbar1 rootClassName="navbar1-root-class-name" :menuItem="menuItem"></app-navbar1>
                <div class="envio01-content-container">
                    <div class="envio01-text-container">
                        <h1 class="envio01-text">
                            <span class="envio01-text01">¡Gracias por preferirnos!</span>
                        </h1>
                        <h1 class="envio01-text">
                            <span class="envio01-text02">Aqui estan todos los envios que a hecho con nosotros</span>
                        </h1>
                    </div>
                    <div>
                        <div id="conteinarSession" class="historial-card-container-secion">
                            <div v-for="envio in envios" :key="envio.id_envio" class="historial-card">
                                <h1 class="historial-text06">
                                    <span>ID: </span>
                                    <span>{{ envio.id_envio }}</span>
                                    <br />
                                </h1>
                                <span class="historial-text09">
                                    <span>Prestadora de servicio</span>
                                    <br />
                                </span>
                                <h1 class="historial-text12">{{ envio.companyName }}</h1>
                                <span class="historial-text13">
                                    <span>Estado</span>
                                    <br />
                                </span>
                                <h1 class="historial-text16">{{ envio.status_paquete }}</h1>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios';

import AppSidelbar from '../components/sidelbar.vue'
import AppNavbar1 from '../components/navbar1.vue'

export default {
    name: 'Envio01',
    props: {},
    components: {
        AppSidelbar,
        AppNavbar1,
    },
    data() {
        return {

            menuItem: "Historial",

            rawdq25: ' ',
            rawd42b: ' ',
            raw685r: ' ',
            rawm9hm: ' ',
            rawf20f: ' ',

            envios: [],
        }
    },

    async mounted() {

        axios.defaults.headers.common['Authorization'] = 'Bearer ' + localStorage.getItem('token');

        await axios.get('https://backend-helptravel-production.up.railway.app/api/getEnvio')
            .then(respuesta => {
                console.log(this.envios = respuesta.data.cart);
            })
            .catch(error => {
                this.$swal({
                    title: 'ERROR',
                    text: '¡Lista de Envio fallando!',
                    icon: 'warning',
                    confirmButtonColor: 'red',
                });
            });
    }
}
</script>
  
<style scoped>
.envio01-container {
    width: 100%;
    display: flex;
    overflow: auto;
    min-height: 100vh;
    align-items: center;
    padding-right: var(--dl-space-space-halfunit);
    flex-direction: column;
    padding-bottom: var(--dl-space-space-halfunit);
    background-color: #DDDDDD;
}

.envio01-max-width {
    width: 100%;
    height: auto;
    display: flex;
    align-self: center;
    padding-top: 0px;
    padding-left: 0px;
    padding-right: 0px;
    flex-direction: row;
    padding-bottom: var(--dl-space-space-unit);
}

.envio01-container-sidelbar {
    width: 210px;
    height: auto;
    display: flex;
    align-items: flex-start;
    flex-direction: column;
}

.envio01-menu-container {
    width: 970px;
    height: auto;
    display: flex;
    align-items: center;
    flex-direction: column;
}

.envio01-content-container {
    flex: 0 0 auto;
    width: 100%;
    height: auto;
    display: flex;
    padding: var(--dl-space-space-oneandhalfunits);
    align-self: center;
    align-items: flex-start;
    border-radius: 16px;
    flex-direction: column;
    background-color: #EEEEEE;
}

.envio01-text-container {
    flex: 0 0 auto;
    width: auto;
    height: auto;
    display: flex;
    padding: var(--dl-space-space-unit);
    align-self: flex-start;
    box-shadow: 5px 5px 10px 0px #d4d4d4;
    align-items: flex-start;
    border-radius: var(--dl-radius-radius-radius8);
    margin-bottom: var(--dl-space-space-unit);
    flex-direction: column;
    background-color: var(--dl-color-gray-white);
}

.envio01-text {
    width: 100%;
    height: 100%;
    font-size: 20px;
    font-family: Open Sans;
    margin-bottom: var(--dl-space-space-unit);
}

.envio01-text01 {
    color: var(--dl-color-backgrounds-primary);
}

.envio01-text02 {
    color: black;
}

.historial-card-container-secion {
    flex: 0 0 auto;
    width: auto;
    height: auto;
    display: flex;
    padding: var(--dl-space-space-unit);
    align-self: flex-start;
    box-shadow: 5px 5px 10px 0px #d4d4d4;
    align-items: flex-start;
    border-radius: var(--dl-radius-radius-radius8);
    margin-bottom: var(--dl-space-space-unit);
    flex-direction: column;
    background-color: var(--dl-color-gray-white);
}

.historial-card {
    width: 855px;
    height: 99px;
    display: flex;
    position: relative;
    box-shadow: 0px 0px 30px 10px #d4d4d4;
    margin-top: var(--dl-space-space-unit);
    transition: 0.3s;
    align-items: flex-start;
    margin-left: var(--dl-space-space-unit);
    border-radius: 34px;
    flex-direction: row;
}

.historial-text06 {
    font-family: Open Sans;
    font-size: 18px;
    align-self: center;
    margin-top: 10px;
    margin-left: var(--dl-space-space-twounits);
}

.historial-text09 {
    font-family: Open Sans;
    font-size: 24px;
    align-self: flex-start;
    margin-top: var(--dl-space-space-unit);
    margin-left: 40px;
    font-weight: 700;
}

.historial-text12 {
    font-family: Open Sans;
    top: 45px;
    left: 253px;
    color: var(--dl-color-grays-gray100);
    margin-top: 5px;
    position: absolute;
    font-size: 18px;
}

.historial-text13 {
    font-family: Open Sans;
    font-size: 24px;
    align-self: flex-start;
    margin-top: var(--dl-space-space-unit);
    margin-left: 98px;
    font-weight: 700;
}

.historial-text16 {
    font-family: Open Sans;
    top: 47px;
    left: 560px;
    color: var(--dl-color-backgrounds-primary);
    position: absolute;
    font-size: 18px;
}
</style>
  