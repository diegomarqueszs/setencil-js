# Introdução
Este é um repositório de estudos sobre StencilJS, um compilador de componentes web que gera web components. O curso é ministrado por [Maximilian Schwarzmüller](https://www.udemy.com/course/web-components-stenciljs-build-custom-html-elements) na Udemy.

## Organização do repositório
O repositório está organizado em pastas, cada uma representando um módulo do curso. Tendo a seguinte estrutura:
```js
   ├── basic-stencil // Módulo 1
   ├── basics-web-components // Módulo 2
   ├── more-complex-components // Módulo 3
   ├── introduction-stenciljs // Módulo 4
   │   └── web-components-stencil
   ├── advanced-stencil // Módulo 5
   │   └── advanced-web-components
   └── shared-web-components // Módulo 6
       ├── example-projects
       └── shared-web-components

```

## Tecnologias
- StencilJS
- Web Components
- TypeScript
- React
- Angular
- Vue

## Informações sobre StencilJS
- Web components são formados por 4 tecnologias: Custom Elements, Shadow DOM, HTML Templates e HTML Imports.
    - Custom Elements: Permite criar elementos HTML personalizados.
    - Shadow DOM: Permite criar um escopo isolado para o HTML e CSS.
    - HTML Templates: Permite criar templates HTML.
    - HTML Imports: Permite importar HTML em outros HTML.

## Adaptação do curso
No curso utilziase a API Alpha Vantage para buscar informações sobre ações. Como a API é paga, as requisoções são limitadas a 25 por dia. É possivel utilizar a API do [ViaCep](https://viacep.com.br/) para buscar informações sobre endereços. A API é gratuita e não requer autenticação. Isso permite o andamento do curso no primeiro web component. Para fazer isso basta substituir a URL da requisição na função `fetch` do arquivo `stock-price.ts` por `https://viacep.com.br/ws/${stockSymbol}/json/` e mudar o tipo de `fetchedPrice` para string. Exemplo:
```ts
fetchStockPrice(stockSymbol: string) {
    this.loading = true;
    fetch(
      `https://viacep.com.br/ws/${stockSymbol}/json/`
    )
      .then(res => {
        if (res.status !== 200) {
          throw new Error('Invalid!');
        }
        return res.json();
      })
      .then(parsedRes => {
        if (!parsedRes['localidade']) {
          throw new Error('Invalid symbol!');
        }
        this.error = null;
        this.fetchedPrice = +parsedRes['localidade']; // Mudar para string
        this.loading = false;
      })
      .catch(err => {
        this.error = err.message;
        this.fetchedPrice = null;
        this.loading = false;
      });
  }

```
> Nota: Também é necessário mudar a busca no arquivo json para `localidade` ou outro campo que deseje.
> ```js
> // Exemplo de resposta da API ViaCep
>{
>  "cep": "01001-000",
>  "logradouro": "Praça da Sé",
>  "complemento": "lado ímpar",
>  "bairro": "Sé",
>  "localidade": "São Paulo",
>  "uf": "SP",
>  "ibge": "3550308",
>  "gia": "1004",
>  "ddd": "11",
>  "siafi": "7107"
>}
>```