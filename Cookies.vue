<template>
    <div>
        <div class="cookies box" v-if="accept">
            <div v-if="config_cookies" class="content">
                <div class="title">Controle sua privacidade</div>
                <div class="text">Utilizamos cookies com objetivo de prover a melhor experiência no uso de nossos serviços. Ao clicar em “Aceitar”, concorda com a utilização de TODOS os cookies.</div>
                <div class="links">
                    <a>Politica de privacidade</a>
                </div>
                <div class="buttons">
                    <div class="gray" v-on:click="config_cookies = false, cookies_options = true">
                        <div>Configurações</div>
                    </div>
                    <div class="green" v-on:click="accept = false">
                        <div>Aceito</div>
                    </div>
                </div>
            </div>
            <div v-if="cookies_options" class="content">
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
                                <input type="checkbox" disabled name="onoffswitch" class="onoffswitch-checkbox" id="myonoffswitch1" tabindex="0" checked>
                                <label class="onoffswitch-label" for="myonoffswitch1">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                    <div class="col-xs-8 infos">
                        <div class="config_title">Cookies Essenciais</div>
                        <div class="config_text">Esses cookies permitem funcionalidades essências, tais como segurança, verificação de identidade e gestão de rede. Esses cookies não podem ser desativados.</div>
                    </div>
                    <div class="col-xs-4 switch">
                        <div>
                            <div class="onoffswitch">
                                <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" id="myonoffswitch2" tabindex="0" checked>
                                <label class="onoffswitch-label" for="myonoffswitch2">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                    <div class="col-xs-8 infos">
                        <div class="config_title">Cookies Essenciais</div>
                        <div class="config_text">Esses cookies permitem funcionalidades essências, tais como segurança, verificação de identidade e gestão de rede. Esses cookies não podem ser desativados.</div>
                    </div>
                    <div class="col-xs-4 switch">
                        <div>
                            <div class="onoffswitch">
                                <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" id="myonoffswitch3" tabindex="0" checked>
                                <label class="onoffswitch-label" for="myonoffswitch3">
                                    <span class="onoffswitch-inner"></span>
                                    <span class="onoffswitch-switch"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="buttons">
                    <div class="links">
                        <a>Politica de privacidade</a>
                    </div>
                    <div class="links">
                        <a>Politica de privacidade</a>
                    </div>
                </div>
                <div class="buttons">
                    <div class="green py-10" v-on:click="config_cookies = true, cookies_options = false">
                        <div>Salvar e aceitar</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped src="./css/cookies.css" lang="css"></style>
<script>
export default {

    data() {
        return {
            config_cookies: true,
            cookies_options:false,
            accept:true
        }
    },
    methods:{

    }
}
</script>
