# Akatsuki CSS

O Akatsuki CSS é um framework CSS flexível e altamente personalizável com uma ampla gama de predefinições. Ele foi projetado para atender a desenvolvedores de todos os níveis de habilidade, proporcionando uma maneira intuitiva de estilizar elementos sem a necessidade de ferramentas adicionais como PostCSS ou JavaScript.

## Recursos

- Elementos facilmente personalizáveis
- Rica coleção de predefinições
- Sem dependência de PostCSS ou JavaScript para personalização
- Livre de dependências

## Como Começar

Para começar a usar o Akatsuki-CSS, siga estas etapas:

### JsDelivr

1. Acesse o site [JsDelivr](https://www.jsdelivr.com/package/npm/yonaka)
2. Copie a tag HTML ou apenas a URL
3. Adicione ao seu código

* HTML

  ```html
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="src/styles/yonaka.css" /> <!--JsDelivr Here on top of the personal CSS-->
    <link rel="stylesheet" href="src/styles/personal.css" /> <!--Personal CSS below here-->
    <title>Cool Example 😎</title>
  </head>
  ```

* CSS

  ```css
  @import url("https://cdn.jsdelivr.net/npm/yonaka/dist/yonaka.min.css");

  /*Sobrescreva os Estilos Aqui*/

  :root {
  --background: tomato;
  }
  ```

### NPM

1. Execute no seu terminal `npm i -D yonaka`

* Se desejar ver o que será baixado, vá para NPM

**Observação:**