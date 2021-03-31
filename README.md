# Componente LGPD 

Componente para atender as demandas da Lei Geral de Proteção de Dados

## Dependencias

- Nuxt;
- Pacote npm "js-cookie"; 

## Como Aplicar

O componente ira gerar os seguintes Cookies : 
```
    :lgpd_load_marketing
    :lgpd_load_analytics
```
Que é possível fazer um get da seguinte forma:
```
    :Cookies.get('lgpd_load_marketing')
    :Cookies.get('lgpd_load_analytics')
```
Eles retornam true ou false, dependendo da escolha do usuário na hora de aceitar os cookies.

Para usar corretamente basta fazer uma verificação das variáveis antes de ativar o uso das ferramentas de analytics e marketing.

## Exemplo de uso no wdshop:

##### Layouts

**_default.vue_**
```
<template>
    ...
    <Lgpd />
    ...
</template>
<script>
import Lgpd from '~/components/Lgpd/Lgpd.vue';
import Cookies from 'js-cookie';

export default {

components: {
    Lgpd
},
mounted(){
    let lgpd_marketing = Cookies.get('lgpd_load_marketing')
    let lgpd_analytics = Cookies.get('lgpd_load_analytics')

    if (this.$wdconfig.default.google_analytics && lgpd_analytics != 'false') {
        let GAID = this.$wdconfig.default.google_analytics
        ;(function (i, s, o, g, r, a, m) {
            i['GoogleAnalyticsObject'] = r
            ;(i[r] =
            i[r] ||
            function () {
                ;(i[r].q = i[r].q || []).push(arguments)
            }),
            (i[r].l = 1 * new Date())
            ;(a = s.createElement(o)), (m = s.getElementsByTagName(o)[0])
            a.async = 1
            a.src = g
            m.parentNode.insertBefore(a, m)
        })(
            window,
            document,
            'script',
            'https://www.googletagmanager.com/gtag/js?id='+GAID,
            'ga'
        )
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', GAID);
    }
    if (this.$wdconfig.default.google_tag_manager && lgpd_marketing === 'true') {
        this.$gtm.init(this.$wdconfig.default.google_tag_manager)
    }
},
...
``` 

## Props
 ##### Nenhuma das props é obrigatória

Para se definir os links corretos das páginas de "Política de privacidade"  e "Política de cookies": 
    * se deixar vazio essas props os links não irão aparecer no modal do componente.
```
    :privacy_policy_link
    :cookies_policy_link
```
O componente também permite a opção de mudança nos textos usando as seguintes props:
    * Se deixar vazio essas props os texto serão os padrões já determinados no componente.    
```
    :essential_text
    :analytics_text
    :marketing_text
```
Opção de botão de configuração do Componente de LGPD. Essa prop aceita true ou false. Se for colocado como true toda vez que o modal estiver fechado, ou seja as configurações desejadas forem salvas, irá aparecer no canto esquerdo da tela um botão para configurar novamento as opções do componente.
```
    :config_button 
``` 
Uma configuração personalizada para abrir o modal novamente seguindo as orientações descritas no próximo bloco:

## Methods

### Configuração personalizada para ativar o modal

Para configurar do jeito que quiser o seu botão para ativar o modal novamente basta executar um evento de click para a seguinte função:

```
    ShowCookies() {
        Cookies.set('lgpd', false)
        sessionStorage.setItem("lgpd_config", false)
        this.$nuxt.$emit('openModal', true)
    }
```

##### Exemplo de uso do componente com as props:

Basta chamar a props no componente e passar o texto:

``` 
<Lgpd :marketing_text="Novo texto" :cookies_policy_link="/politica-de-cookies" />
```


## Comentários sobre o código


##### Salvamento das opções e como evitar o recarregamento da página


```
SaveLGPD(all=false) {
    sessionStorage.setItem("lgpd_config", false)
    let Before_lgpd_marketing = Cookies.get('lgpd_load_marketing')
    let Before_lgpd_analytics = Cookies.get('lgpd_load_analytics')
    Cookies.set('lgpd_load_analytics', this.analytics, { expires: 7} )
    Cookies.set('lgpd_load_marketing', this.marketing, { expires: 7} )
    sessionStorage.setItem("lgpd_config", true)
    if (this.marketing == true && this.analytics == true) {
        Cookies.set('lgpd', true, { expires: 7} )
        if ((Before_lgpd_analytics === undefined && Before_lgpd_marketing === undefined) || (Before_lgpd_analytics === 'true' && Before_lgpd_marketing === 'true') ) {
            all = true
        }
    }
    if(!all) {
        location.reload()
    }            
    this.closeBox()
},
```

Esse trecho do código foi adaptado assumindo que as ferramentas que irão precisar de autorização do usuário ja comecem iniciadas, mesmo que nenhuma configuração no componente tenha sido feita. Assim ele verifica se os cookies ja foram definidos ou não para tomar a decisão de fazer o recaregamento da página.
Se os cookies estavam indefinidos, ou seja primeira vez no site e clicou no botão de configurações e aceitou com todas opções aceitas ele não recarrega a página ou se ele ja aceitou os cookies mas clicou para configurar e deixou tudo aceito de novo, ainda sim não recarrega a página.
Se o usuário clicar no primeiro botão de aceito, a página tambem não vai ser recarregada e irá setar os cookies para guardar a informação.
Só vai recarrecar a página se um deles for desativado.




## License

WdHouse 
