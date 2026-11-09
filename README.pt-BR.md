# Yonaka

[English](README.md) | [Português](README.pt-BR.md)

O Yonaka é um framework CSS flexível e altamente personalizável, com uma ampla gama de estilos prontos. Ele foi projetado para atender desenvolvedores de todos os níveis, oferecendo uma maneira intuitiva de estilizar elementos sem ferramentas adicionais como PostCSS ou JavaScript.

> Este guia cobre apenas o início rápido. Para a documentação completa (variáveis, componentes, utilitários e temas), veja o [README em inglês](README.md).

## Recursos

- Elementos fáceis de personalizar
- Rica coleção de estilos prontos
- Sem dependência de PostCSS ou JavaScript para personalizar (para quem usa o framework)
- Livre de dependências

## Como começar

Para começar a usar o Yonaka, siga os passos abaixo.

### Instalação

#### jsDelivr

1. Acesse o site do [jsDelivr](https://www.jsdelivr.com/package/npm/yonaka)
2. Copie a tag HTML ou apenas a URL
3. Adicione ao seu código

**HTML**

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/yonaka/dist/yonaka.css" /> <!--jsDelivr aqui, antes do seu CSS-->
  <link rel="stylesheet" href="src/styles/personal.css" /> <!--Seu CSS abaixo-->
  <title>Exemplo legal 😎</title>
</head>
```

**CSS**

```css
@import url("https://cdn.jsdelivr.net/npm/yonaka/dist/yonaka.css");

/* Sobrescreva os estilos aqui */

:root {
  --background: tomato;
}
```

#### npm

1. Execute no terminal:

   ```bash
   npm i yonaka
   ```

   Se quiser ver o que será instalado, acesse o [npm](https://www.npmjs.com/package/yonaka).

2. Importe o Yonaka no seu código (igual à opção do jsDelivr):

**HTML**

```html
<link rel="stylesheet" href="node_modules/yonaka/dist/yonaka.css" />
<link rel="stylesheet" href="src/styles/personal.css" />
```

**CSS**

```css
@import url("node_modules/yonaka/dist/yonaka.css");

:root {
  --background: rebeccapurple;
}
```

**Observação:** respeite a ordem da cascata. O seu CSS deve vir depois do Yonaka para sobrescrever os estilos.

### Estrutura mínima do HTML

```html
<body>
  <header>
    <nav></nav>
  </header>

  <!-- Para ter uma seção hero, coloque-a entre o header e o main -->
  <section class="hero"></section>

  <main></main>

  <footer></footer>
</body>
```

### Tema

As cores seguem a preferência do sistema. Para forçar um tema, use `data-theme="light"` ou `data-theme="dark"` no `<html>`.

## Licença

[MIT](LICENSE.md)
