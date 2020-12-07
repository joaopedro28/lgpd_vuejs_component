<template>
    <div>
        <div class="cookies box" v-show="box">
            <div v-if="config_cookies" class="content">
                <div class="title">Controle sua privacidade</div>
                <div class="text">Utilizamos cookies com objetivo de prover a melhor experiência no uso de nossos serviços. Ao clicar em “Aceitar”, concorda com a utilização de TODOS os cookies.</div>
                <div class="links">
                    <a href="/politica-de-privacidade" >Política de privacidade</a>
                </div>
                <div class="flex-row buttons">
                    <div class="gray pointer" v-on:click="config_cookies = false, cookies_options = true">
                        <div>Configurações</div>
                    </div>
                    <div class="green pointer" v-on:click="SaveLGPD()">
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
                        <div class="config_title">Cookies Essenciais</div>
                        <div class="config_text">Esses cookies permitem funcionalidades essências, tais como segurança, verificação de identidade e gestão de rede. Esses cookies não podem ser desativados.</div>
                    </div>
                    <div class="col-xs-4 switch">
                        <div>
                            <div class="onoffswitch">
                                <input type="checkbox" disabled name="onoffswitch" class="onoffswitch-checkbox" v-model="essenciais" id="myonoffswitch1"  tabindex="0" checked>
                                <label class="onoffswitch-label" for="myonoffswitch1">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                    <div class="col-xs-8 infos">
                        <div class="config_title">Cookies de marketing</div>
                        <div class="config_text">Esses cookies são usados para rastrear a eficácia da publicidade, fornecer um serviço mais relevante e anúncios melhores para atender aos seus interesses.</div>
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
                    <div class="col-xs-8 infos">
                        <div class="config_title">Cookies funcionais</div>
                        <div class="config_text">Esses cookies coletam dados para lembrar escolas que os usuários fazem e para melhorar e proporcionar uma experiência mais personalizada.</div>
                    </div>
                    <div class="col-xs-4 switch">
                        <div>
                            <div class="onoffswitch">
                                <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" v-model="funcionais" id="myonoffswitch3" tabindex="0" >
                                <label class="onoffswitch-label" for="myonoffswitch3">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="flex-row">
                    <div class="links">
                        <a href="/politica-de-privacidade" >Política de privacidade</a>
                    </div>
                    <div class="links ">
                        <a href="/politica-de-privacidade" >Política dos cookies</a>
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
    data() {
        return {
            config_cookies: true,
            cookies_options:false,
            accept:true,
            essenciais:true,
            marketing:true,
            funcionais:true,
            box:false
        }
    },
    mounted() {
        setTimeout(() => {
            this.box = true;
            if (Cookies.get('lgpd') == 'true' || sessionStorage.getItem("lgpd_config") == 'true'){
                this.box = false
            }
        }, 3000);
    },
    methods: {
        SaveLGPD() {
            sessionStorage.setItem("lgpd_config", false)
            Cookies.set('lgpd_load_functional', this.funcionais )
            Cookies.set('lgpd_load_marketing', this.marketing )
            if (this.marketing == true || this.funcionais == true) {
                sessionStorage.setItem("lgpd_config", true)
            }
            if (this.marketing == true && this.funcionais == true) {
                Cookies.set('lgpd', true)
            }
            location.reload()
            this.closeBox()
        },
        closeBox() {
            this.accept =false
        },
    }
}
</script>
