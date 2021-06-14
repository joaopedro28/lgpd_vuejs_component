# Componente LGPD 

Componente para atender as demandas da Lei Geral de Proteção de Dados
#
## Dependencias

- Nuxt;
- Pacote npm "js-cookie"; 
#
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
#
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
}
...
``` 
#
## Props
- #### Nenhuma das props é obrigatória

### Props que são String:

Título principal do componente
```
    <Lgpd :title="" />
```
 - default = Controle sua privacidade 


Texto principal do componente
```
    <Lgpd :text="" />
```
 - default = Utilizamos cookies com objetivo de prover a melhor experiência no uso de nossos serviços. Ao clicar em “Aceitar”, concorda com a utilização de TODOS os cookies.

### Props que são Object:

Textos internos de configurações

```
    <Lgpd :essential_texts="" />
    <Lgpd :marketing_texts="" />
    <Lgpd :analytics_texts="" />

    Exemlo de objeto:
    
    { 
        title: 'Cookies de marketing',
        text:  'Esses cookies são usados para rastrear a eficácia da publicidade, fornecer um serviço mais relevante e anúncios melhores para atender aos seus interesses.'
    }
```

Texto e link das opções de Políticas
```
    <Lgpd :privacy_policy="" />
    <Lgpd :cookies_policy="" />

    Exemlo de objeto:
    
    { 
        title: 'Política de cookies',
        link:  '/politica-de-privacidade'
    }
```
* se deixar vazio essas props os links não irão aparecer no modal do componente.


Texto dos botões do componente:
```
    <Lgpd :buttons="" />

    Exemlo de objeto:
    
    { 
        config:'Configurações',
        accept:'Aceito',
        save_accept:'Aceitar e salvar'
    }
```

### Props que são Boolean:

Opção de botão de configuração do Componente de LGPD.  Se for colocado como true, toda vez que o modal estiver fechado, ou seja as configurações desejadas forem salvas, irá aparecer no canto esquerdo da tela um botão para configurar novamente as opções do componente.
```
        <Lgpd :config_button="true" />
``` 

- default= false

#
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
#
## Comentários sobre o código


### Salvamento das opções e como evitar o recarregamento da página


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



