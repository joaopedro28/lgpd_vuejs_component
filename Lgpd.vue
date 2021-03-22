<template>
    <div>
        <client-only>
            <div class="lgpd_wd_box" v-if="box">
                <div v-if="config_cookies" class="lgpd_wd_content">
                    <div class="lgpd_wd_title">{{title}}</div>
                    <div class="lgpd_wd_text">{{text}}</div>
                    <div class="lgpd_wd_links">
                        <a :href="privacy_policy.link" v-if="privacy_policy.link">{{privacy_policy.title}}</a>
                    </div>
                    <div class="lgpd_wd_flex-row lgpd_wd_buttons">
                        <div class="lgpd_wd_buttons_gray lgpd_wd_pointer" v-on:click="config_cookies = false, cookies_options = true">
                            <div>{{buttons.config}}</div>
                        </div>
                        <div class="lgpd_wd_buttons_green lgpd_wd_pointer " v-on:click="SaveAllLGPD()">
                            <div>{{buttons.accept}}</div>
                        </div>
                    </div>
                </div>
                <div v-if="cookies_options" class="lgpd_wd_content">
                    <div v-on:click="cookies_options=false , config_cookies=true">
                        <div class="lgpd_wd_close lgpd_wd_pointer" >
                            x
                        </div>
                    </div>
                    <div class="lgpd_wd_title">{{title}}</div>
                    <div class="lgpd_wd_display-flex lgpd_wd_flex-row lgpd_wd_my-20">
                        <div class="lgpd_wd_flex-column">
                            <div class="lgpd_wd_infos">
                                <div class="lgpd_wd_config_title">{{essential_texts.title}}</div>
                                <div class="lgpd_wd_config_text">{{essential_texts.text}}</div>
                            </div>
                        </div>
                        <div class="lgpd_wd_switch">
                            <div>
                                <div class="lgpd_wd_onoffswitch">
                                    <input type="checkbox" disabled name="onoffswitch" class="lgpd_wd_onoffswitch-checkbox" v-model="essential" id="myonoffswitch1"  tabindex="0" checked>
                                    <label class="lgpd_wd_onoffswitch-label lgpd_wd_opacity-label" for="myonoffswitch1">
                                        <span class="lgpd_wd_onoffswitch-inner"></span>
                                        <span class="lgpd_wd_onoffswitch-switch"></span>
                                    </label>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="lgpd_wd_display-flex lgpd_wd_flex-row lgpd_wd_my-20">
                        <div class="lgpd_wd_flex-column">
                            <div class="lgpd_wd_infos">
                                <div class="lgpd_wd_config_title">{{analytics_texts.title}}</div>
                                <div class="lgpd_wd_config_text">{{analytics_texts.text}}</div>
                            </div>
                        </div>
                        <div class="lgpd_wd_switch">
                            <div>
                                <div class="lgpd_wd_onoffswitch">
                                    <input type="checkbox" name="onoffswitch" class="lgpd_wd_onoffswitch-checkbox" v-model="analytics" id="myonoffswitch2"  tabindex="0" checked>
                                    <label class="lgpd_wd_onoffswitch-label" for="myonoffswitch2">
                                        <span class="lgpd_wd_onoffswitch-inner"></span>
                                        <span class="lgpd_wd_onoffswitch-switch"></span>
                                    </label>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="lgpd_wd_display-flex lgpd_wd_flex-row lgpd_wd_my-20">
                        <div class="lgpd_wd_infos">
                            <div class="lgpd_wd_config_title">{{marketing_texts.title}}</div>
                            <div class="lgpd_wd_config_text">{{marketing_texts.text}}</div>
                        </div>
                        <div class="lgpd_wd_switch">
                            <div>
                                <div class="lgpd_wd_onoffswitch">
                                    <input type="checkbox" name="onoffswitch" class="lgpd_wd_onoffswitch-checkbox" v-model="marketing" id="myonoffswitch3"  tabindex="0" checked>
                                    <label class="lgpd_wd_onoffswitch-label" for="myonoffswitch3">
                                        <span class="lgpd_wd_onoffswitch-inner"></span>
                                        <span class="lgpd_wd_onoffswitch-switch"></span>
                                    </label>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="lgpd_wd_flex-row">
                        <div class="lgpd_wd_links">
                            <div class="lgpd_wd_flex-row lgpd_wd_align-items-center" v-if="privacy_policy.link || cookies_policy.link" >
                                <div class="lgpd_wd_links" v-if="privacy_policy.link">
                                    <a class="lgpd_wd_mx-20" :href="privacy_policy.link">{{privacy_policy.title}}</a>
                                </div>
                                <div class="lgpd_wd_links" v-if="cookies_policy.link">
                                    <a class="lgpd_wd_mx-20" :href="cookies_policy.link">{{cookies_policy.title}}</a>
                                </div>
                            </div>
                            <div class="lgpd_wd_buttons-config">
                                <div class="lgpd_wd_butons_green lgpd_wd_pointer" v-on:click="SaveLGPD()">
                                    <div>{{buttons.save_accept}}</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div  v-if="InitBox && !box && config_button">
                <div class="lgpd_wd_config"  >
                    <a href="#" @click.prevent="ShowCookies()">
                        <svg xmlns="http://www.w3.org/2000/svg" width="35px" height="35px" version="1.1" viewBox="-38 0 511 511.99956" >
                            <g id="surface1">
                            <path d="M 413.476562 341.910156 C 399.714844 379.207031 378.902344 411.636719 351.609375 438.289062 C 320.542969 468.625 279.863281 492.730469 230.699219 509.925781 C 229.085938 510.488281 227.402344 510.949219 225.710938 511.289062 C 223.476562 511.730469 221.203125 511.96875 218.949219 512 L 218.507812 512 C 216.105469 512 213.691406 511.757812 211.296875 511.289062 C 209.605469 510.949219 207.945312 510.488281 206.339844 509.9375 C 157.117188 492.769531 116.386719 468.675781 85.289062 438.339844 C 57.984375 411.6875 37.175781 379.277344 23.433594 341.980469 C -1.554688 274.167969 -0.132812 199.464844 1.011719 139.433594 L 1.03125 138.511719 C 1.261719 133.554688 1.410156 128.347656 1.492188 122.597656 C 1.910156 94.367188 24.355469 71.011719 52.589844 69.4375 C 111.457031 66.152344 156.996094 46.953125 195.90625 9.027344 L 196.246094 8.714844 C 202.707031 2.789062 210.847656 -0.117188 218.949219 0.00390625 C 226.761719 0.105469 234.542969 3.007812 240.773438 8.714844 L 241.105469 9.027344 C 280.023438 46.953125 325.5625 66.152344 384.429688 69.4375 C 412.664062 71.011719 435.109375 94.367188 435.527344 122.597656 C 435.609375 128.386719 435.757812 133.585938 435.988281 138.511719 L 436 138.902344 C 437.140625 199.046875 438.554688 273.898438 413.476562 341.910156 Z M 413.476562 341.910156 " style="stroke:none;fill-rule:nonzero;fill: rgb(34 126 0);fill-opacity:1;" data-v-0df40038=""></path>
                            <path d="M 346.101562 256 C 346.101562 326.207031 289.097656 383.355469 218.949219 383.605469 L 218.5 383.605469 C 148.144531 383.605469 90.894531 326.359375 90.894531 256 C 90.894531 185.644531 148.144531 128.398438 218.5 128.398438 L 218.949219 128.398438 C 289.097656 128.648438 346.101562 185.796875 346.101562 256 Z M 346.101562 256 " style=" stroke:none;fill-rule:nonzero;fill:rgb(100%,100%,100%);fill-opacity:1;" data-v-0df40038=""></path>
                            <path d="M 276.417969 237.625 L 218.949219 295.101562 L 206.53125 307.519531 C 203.597656 310.453125 199.75 311.917969 195.90625 311.917969 C 192.058594 311.917969 188.214844 310.453125 185.277344 307.519531 L 158.578125 280.808594 C 152.710938 274.941406 152.710938 265.4375 158.578125 259.566406 C 164.4375 253.699219 173.953125 253.699219 179.820312 259.566406 L 195.90625 275.652344 L 255.175781 216.382812 C 261.042969 210.511719 270.558594 210.511719 276.417969 216.382812 C 282.285156 222.25 282.285156 231.765625 276.417969 237.625 Z M 276.417969 237.625 " style="stroke:none;fill-rule:nonzero;fill: rgb(34 126 0);fill-opacity:1;" data-v-0df40038=""></path>
                            </g>
                        </svg>
                    </a>
                </div>
            </div>
        </client-only>
    </div>
</template>
<style scoped src="./css/lgpd.css" lang="css"></style>
<script>
import Cookies from 'js-cookie';

export default {
    props:{
		title:{
			type: String,
            required:false,
            default:'Controle sua privacidade'
		},
		text:{
			type: String,
            required:false,
            default:'Utilizamos cookies com objetivo de prover a melhor experiência no uso de nossos serviços. Ao clicar em “Aceitar”, concorda com a utilização de TODOS os cookies.'
		},
		config_button: {
            type: Boolean,
            require: false,
            default: false
		},
		essential_texts:{
			type:Object,
			require:false,
			default: () => ({
				title: 'Cookies essenciais e funcionais',
				text:'Esses cookies permitem funcionalidades essências, tais como segurança, verificação de identidade e gestão de rede. Esses cookies não podem ser desativados.',
			})
		},
		analytics_texts:{
			type:Object,
			require:false,
			default: () => ({
				title: 'Cookies de desempenho e analíticos',
				text:'Esses cookies coletam dados para lembrar escolhas que os usuários fazem e para melhorar e proporcionar uma experiência mais personalizada.'
			})
		},
		marketing_texts:{
			type:Object,
			require:false,
			default: () => ({
				title: 'Cookies de marketing',
				text: 'Esses cookies são usados para rastrear a eficácia da publicidade, fornecer um serviço mais relevante e anúncios melhores para atender aos seus interesses.',
			})
		},
		privacy_policy: {
			type: Object,
			require:false,
			default: () => ({
				title:'Política de privacidade',
				link: ''
			})
		},
        cookies_policy: {
			type: Object,
			require:false,
			default: () => ({
				title:'Política de cookies',
				link: ''
			})
		},
		buttons:{
			type: Object,
			require:false,
			default: () => ({
				config:'Configurações',
				accept:'Aceito',
				save_accept:'Aceitar e salvar'
			})
		}
    },
    data() {
        return {
            config_cookies: true,
            cookies_options:false,
            accept:true,
            essential:true,
            marketing:'',
            analytics:'',
            box:false
        }
    },
    mounted() {
        this.analytics = true
        this.marketing = true
        if (Cookies.get('lgpd_load_marketing') != undefined) {
            this.marketing = Cookies.get('lgpd_load_marketing') == 'true' ? true : false
            this.analytics = Cookies.get('lgpd_load_analytics') == 'true' ? true : false
        }
        setTimeout(() => {
            this.box = true;
            if (Cookies.get('lgpd') == 'true' || sessionStorage.getItem("lgpd_config") == 'true'){
                this.box = false
            }
        }, 2000);
        this.$nuxt.$on("openModal", () => {
            this.box = true;
        });
    },
    methods: {
        SaveLGPD() {
            sessionStorage.setItem("lgpd_config", false)
            Cookies.set('lgpd_load_analytics', this.analytics, { expires: 7} )
            Cookies.set('lgpd_load_marketing', this.marketing, { expires: 7} )
            sessionStorage.setItem("lgpd_config", true)
            if (this.marketing == true && this.analytics == true) {
                Cookies.set('lgpd', true, { expires: 7} )
            }
            // location.reload()
            this.closeBox()
        },
        SaveAllLGPD() {
            this.marketing = true
            this.analytics = true
            this.SaveLGPD()
        },
        closeBox() {
            this.box =false
        },
        ShowCookies() {
            Cookies.set('lgpd', false)
            sessionStorage.setItem("lgpd_config", false)
            this.$nuxt.$emit('openModal', true)
        }
    },
    computed: {
        InitBox(){
            if (Cookies.get('lgpd')) {
                if (Cookies.get('lgpd') === undefined) {
                    return false
                }
            }
            return true
        },
    }
}
</script>
