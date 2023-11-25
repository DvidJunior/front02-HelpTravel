<template>
    <div class="envio01-container">
        <div class="envio01-max-width">
            <div class="envio01-container-sidelbar">
                <app-sidelbar></app-sidelbar>
                <router-view />
            </div>
            <div class="envio01-menu-container">
                <app-navbar1 rootClassName="navbar1-root-class-name" :menuItem="menuItem" :heading1="nameUsu"></app-navbar1>
                <div class="envio01-content-container">
                    <div class="envio01-text-container">
                        <h1 class="envio01-text">
                            <span class="envio01-text01">¡Gracias por preferirnos!</span>
                        </h1>
                        <h1 class="envio01-text">
                            <span class="envio01-text02">Aqui estan todos los envios que a hecho con nosotros</span>
                        </h1>
                    </div>
                    <div class="historial-container-text-card">
                        <div class="historial-card-container">
                            <div id="conteinarSession" class="historial-blog">
                                <div v-for="envio in envios" :key="envio.id_envio" class="historial-container1">

                                    <div class="historial-blog-post-card">
                                        <img alt="image"
                                            src="https://images.unsplash.com/photo-1487553333251-6c8e26d3dc2c?ixid=Mnw5MTMyMXwwfDF8c2VhcmNofDU2fHwlMjBwbGFuZXxlbnwwfHx8fDE2Njg4NTI5MjA&amp;ixlib=rb-4.0.3&amp;h=400"
                                            image_src="https://images.unsplash.com/photo-1487553333251-6c8e26d3dc2c?ixid=Mnw5MTMyMXwwfDF8c2VhcmNofDU2fHwlMjBwbGFuZXxlbnwwfHx8fDE2Njg4NTI5MjA&amp;ixlib=rb-4.0.3&amp;h=400"
                                            class="historial-image" />
                                        <div class="historial-container2">
                                            <div class="historial-container3">
                                                <span class="historial-text10">[ ENVIO ]</span>
                                                <span class="historial-text11">{{ formatearFecha(envio.create_at) }}</span>
                                            </div>
                                            <h1 class="historial-text12">[ {{ envio.companyName }} ]</h1>
                                            <div class="historial-container4">
                                                <div class="historial-container5">
                                                    <h1 class="historial-text13">[ Destino ]</h1>
                                                    <span class="historial-text14">[{{ envio.destinoCiudad }}][{{ envio.destinoDir }}]</span>
                                                </div>
                                                <div class="historial-container6">
                                                    <h1 class="historial-text15">[ Total ]</h1>
                                                    <span class="historial-text18">[{{ envio.precioTotal }}]</span>
                                                </div>
                                                <div class="historial-container7">
                                                    <h1 class="historial-text17">[ Estado ]</h1>
                                                    <span class="historial-text18">[{{ envio.status_paquete }}]</span>
                                                </div>
                                            </div>

                                        </div>
                                    </div>

                                </div>
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
import {format} from 'date-fns';

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

            nameUsu: '',

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

        await axios.get('https://backend-helptravel-production.up.railway.app/api/user')
            .then(respuesta => {
                this.nameUsu = respuesta.data.email
            })
            .catch(error => {
                this.$swal({
                    title: 'ERROR',
                    text: '¡Upss paso algo el nombre del ususario!',
                    icon: 'warning',
                    confirmButtonColor: 'red',
                });
            });
    },
    methods: {
        formatearFecha(fecha) {
            return format(new Date(fecha), 'yyyy-MM-dd');
        },
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

.historial-text12 {
  font-size: 20px;
  font-family: "Open Sans";
  margin-bottom: var(--dl-space-space-twounits);
}

.historial-text13 {
  font-size: 18px;
  align-self: center;
  margin-right: 300px;
}

.historial-text16 {
    font-family: Open Sans;
    top: 47px;
    left: 560px;
    color: var(--dl-color-backgrounds-primary);
    position: absolute;
    font-size: 18px;
}

.historial-container-text-card {
    flex: 0 0 auto;
    width: 100%;
    height: auto;
    display: flex;
    box-shadow: 5px 5px 10px 0px #d4d4d4;
    align-items: flex-start;
    flex-direction: row;
}

.historial-card-container {
    flex: 0 0 auto;
    width: 100%;
    display: flex;
    padding: var(--dl-space-space-unit);
    align-self: center;
    align-items: flex-start;
    margin-left: 0px;
    border-radius: var(--dl-radius-radius-radius8);
    flex-direction: column;
    justify-content: center;
    background-color: var(--dl-color-gray-white);
    border-top-left-radius: 0px;
}

.historial-blog {
    width: 100%;
    display: flex;
    padding: var(--dl-space-space-threeunits);
    max-width: var(--dl-size-size-maxwidth);
    align-items: center;
    flex-direction: column;
    justify-content: space-between;
}

.historial-container1 {
    display: flex;
    align-items: center;
    margin-bottom: var(--dl-space-space-twounits);
    flex-direction: column;
    justify-content: space-between;
}

.historial-blog-post-card {
    width: 100%;
    display: flex;
    max-width: var(--dl-size-size-maxwidth);
    box-shadow: 4px 4px 10px 0px rgba(18, 18, 18, 0.1);
    transition: 0.3s;
    align-items: stretch;
    flex-direction: row;
    justify-content: space-between;
}

.historial-blog-post-card:hover {
    transform: scale(1.02);
}

.historial-image {
    width: 199px;
    height: 173px;
    align-self: center;
    margin-top: var(--dl-space-space-unit);
    object-fit: cover;
    flex-shrink: 0;
    border-radius: 16px;
    margin-bottom: var(--dl-space-space-unit);
}

.historial-container2 {
    display: flex;
    align-items: flex-start;
    padding-top: var(--dl-space-space-twounits);
    padding-left: var(--dl-space-space-twounits);
    padding-right: var(--dl-space-space-twounits);
    flex-direction: column;
    padding-bottom: var(--dl-space-space-twounits);
    justify-content: space-between;
}

.historial-container3 {
    width: 100%;
    display: flex;
    align-items: flex-start;
    margin-bottom: var(--dl-space-space-halfunit);
    flex-direction: row;
    justify-content: space-between;
}

.historial-text10 {
    color: rgb(89, 89, 89);
    font-weight: 600;
    text-transform: uppercase;
}

.historial-text11 {
    color: #595959;
    font-weight: 300;
}

.historial-text12 {
    font-size: 20px;
    font-family: "Open Sans";
    margin-bottom: var(--dl-space-space-twounits);
}

.historial-container4 {
    flex: 0 0 auto;
    width: auto;
    display: flex;
    align-items: flex-start;
    margin-bottom: var(--dl-space-space-twounits);
    flex-direction: column;
}

.historial-container5 {
    flex: 0 0 auto;
    width: 100%;
    height: auto;
    display: flex;
    margin-top: var(--dl-space-space-unit);
    align-items: flex-start;
    margin-bottom: var(--dl-space-space-unit);
}

.historial-text13 {
    font-size: 18px;
    align-self: center;
    margin-right: 50px;
}

.historial-text14 {
    color: rgb(89, 89, 89);
    font-size: 18px;
    align-self: center;
    font-family: "Open Sans";
}

.historial-container6 {
    flex: 0 0 auto;
    width: 100%;
    height: auto;
    display: flex;
    align-items: flex-start;
    margin-bottom: var(--dl-space-space-unit);
}

.historial-text15 {
    font-size: 18px;
    align-self: center;
    margin-right: 200px;
}

.historial-text16 {
    color: rgb(89, 89, 89);
    font-size: 18px;
    align-self: center;
    font-family: "Open Sans";
}

.historial-container7 {
    flex: 0 0 auto;
    width: 100%;
    height: auto;
    display: flex;
    align-items: flex-start;
}

.historial-text17 {
    font-size: 18px;
    align-self: center;
    margin-right: 200px;
}

.historial-text18 {
    color: rgb(89, 89, 89);
    font-size: 18px;
    align-self: center;
    font-family: "Open Sans";
}

@media(max-width: 991px) {
    .historial-blog-post-card {
        flex-direction: row;
        justify-content: space-between;
    }
}

@media(max-width: 767px) {
    .historial-blog {
        padding-left: var(--dl-space-space-twounits);
        padding-right: var(--dl-space-space-twounits);
    }

    .historial-blog-post-card {
        flex-direction: column;
    }

    .historial-image {
        width: 100%;
    }
}

@media(max-width: 479px) {
    .historial-blog {
        padding-top: var(--dl-space-space-twounits);
        padding-left: var(--dl-space-space-unit);
        padding-right: var(--dl-space-space-unit);
        padding-bottom: var(--dl-space-space-twounits);
    }
}</style>
  