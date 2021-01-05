# Componente LGPD 

Componente para atender as demandas da Lei Geral de Proteção de Dados

## Dependencias

- Nuxt;
- Pacote npm "js-cookie"; 

## Como Aplicar

O componente ira gerar os seguintes Cookies : 

    - lgpd_load_marketing
    - lgpd_load_analytics

Que é possível fazer um get da seguinte forma:

    - Cookies.get('lgpd_load_marketing')
    - Cookies.get('lgpd_load_analytics')

Eles retornam true ou false, dependendo da escolha do usuário na hora de aceitar os cookies.

Para usar corretamente basta fazer uma verificação das variáveis antes de ativar o uso das ferramentas de analytics e marketing.

## Exemplo de uso no wdshop:

#####Layouts
**_default.vue_**
```
import Lgpd from '~/components/Lgpd/Lgpd.vue';
import Cookies from 'js-cookie';

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

O componente também permite a opção de mudança nos textos usando as seguintes props:

- essential_text
- analytics_text
- marketing_text

Basta chamar a props no componente e passar o texto:

<Lgpd :marketing_text="Novo texto" />

## License

WdHouse 
