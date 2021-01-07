<template>
    <div>
        <div class="lgpd_wd box" v-show="box">
            <div v-if="config_cookies" class="content">
                <div class="title">Controle sua privacidade</div>
                <div class="text">Utilizamos cookies com objetivo de prover a melhor experiência no uso de nossos serviços. Ao clicar em “Aceitar”, concorda com a utilização de TODOS os cookies.</div>
                <div class="links">
                    <a :href="privacy_policy_link" v-if="privacy_policy_link">Política de privacidade</a>
                </div>
                <div class="flex-row buttons">
                    <div class="gray pointer" v-on:click="config_cookies = false, cookies_options = true">
                        <div>Configurações</div>
                    </div>
                    <div class="green pointer" v-on:click="SaveAllLGPD()">
                        <div>Aceito</div>
                    </div>
                </div>
            </div>
            <div v-if="cookies_options" class="content">
                <div v-on:click="cookies_options=false , config_cookies=true">
                    <div class="close" >
                        X
                    </div>
                </div>
                <div class="row">
                    <div class="col-xs-12">
                        <div class="title">Controle sua privacidade</div>
                    </div>
                    <div class="col-xs-8 infos">
                        <div class="config_title">Cookies essenciais e funcionais</div>
                        <div class="config_text">{{essential_text}}</div>
                    </div>
                    <div class="col-xs-4 switch">
                        <div>
                            <div class="onoffswitch">
                                <input type="checkbox" disabled name="onoffswitch" class="onoffswitch-checkbox" v-model="essential" id="myonoffswitch1"  tabindex="0" checked>
                                <label class="onoffswitch-label" for="myonoffswitch1">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                    <div class="col-xs-8 infos">
                        <div class="config_title">Cookies de desempenho e analíticos</div>
                        <div class="config_text">{{analytics_text}}</div>

                    </div>
                    <div class="col-xs-4 switch">
                        <div>
                            <div class="onoffswitch">
                                <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" v-model="analytics" id="myonoffswitch3" tabindex="0" >
                                <label class="onoffswitch-label" for="myonoffswitch3">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                    <div class="col-xs-8 infos">
                        <div class="config_title">Cookies de marketing</div>
                        <div class="config_text">{{marketing_text}}</div>
                    </div>
                    <div class="col-xs-4 switch">
                        <div>
                            <div class="onoffswitch">
                                <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" v-model="marketing" id="myonoffswitch2" tabindex="0" >
                                <label class="onoffswitch-label" for="myonoffswitch2">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="flex-row align-items-center" v-if="privacy_policy_link || cookies_policy_link" >
                    <div class="links" v-if="privacy_policy_link">
                        <a :href="privacy_policy_link" >Política de privacidade</a>
                    </div>
                    <div class="links " v-if="cookies_policy_link">
                        <a :href="cookies_policy_link" >Política dos cookies</a>
                    </div>
                </div>
                <div class="buttons-config">
                    <div class="green pointer py-10" v-on:click="SaveLGPD()">
                        <div>Salvar e aceitar</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped src="./css/lgpd.css" lang="css"></style>
<script>
import Cookies from 'js-cookie';

export default {
    props:{
        essential_text:{
            required:false,
            default:'Esses cookies permitem funcionalidades essências, tais como segurança, verificação de identidade e gestão de rede. Esses cookies não podem ser desativados.'
        },
        analytics_text:{
            required:false,
            default:'Esses cookies coletam dados para lembrar escolhas que os usuários fazem e para melhorar e proporcionar uma experiência mais personalizada.'
        },
        marketing_text:{
            required:false,
            default:'Esses cookies são usados para rastrear a eficácia da publicidade, fornecer um serviço mais relevante e anúncios melhores para atender aos seus interesses.'
        },
        privacy_policy_link: {
            require:false,
            default:false
        },
        cookies_policy_link: {
            require:false,
            default:false
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
            Cookies.set('lgpd_load_analytics', this.analytics )
            Cookies.set('lgpd_load_marketing', this.marketing )
            sessionStorage.setItem("lgpd_config", true)
            if (this.marketing == true && this.analytics == true) {
                Cookies.set('lgpd', true)
            }
            location.reload()
            this.closeBox()
        },
        SaveAllLGPD() {
            this.marketing = true
            this.analytics = true
            this.SaveLGPD()
        },
        closeBox() {
            this.accept =false
        },
    }
}
</script>
