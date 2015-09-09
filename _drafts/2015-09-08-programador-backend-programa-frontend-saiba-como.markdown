---
title:  "Programador Backend programa Frontend, saiba como:"
date:   2015-09-07 10:18:00
description: Como sobreviver no mundo frontend sendo um programador backend e ganhar o titulo de programador full stack
---

primeiro post no blog, _estou muito neuvosor_

Nesse post vou explicar como manter sua sanidade tirando onda em um frontend totalmente agnostico com [Angular.js][angular-doc] e [Browserify][browserify] + [Babelify][babeljs](ES6 transpiler), e sendo um hipster descolado com [Gulp][gulp]. E, de quebra, ver como configurar o gulp para o [LESS][less-docs] e alguns pitacos de [Ramda.js][ramda-docs].

## Requisitos

### Antes de tudo nesse post será necessário conhecimento nas seguintes tecnologias:

- sobre sua command line preferida, seja ela no GNU/Linux, *BSD, OSX, Windows ou no seu artefato eletronico predileto;
- [Javascript][javascript-doc];
- HTML;
- [Angular.js][angular-doc].

### E também será necessário ter instalado em seu PC:

- [Node.js][nodejs-download];
- NPM(se você baixar o instalador no website do Node.js não precisa instalar o NPM pois já vem junto, você pode verificar executando `npm` no _terminal_);
- [Python 2.7.x][python-download](necessário para alguns pacotes do NPM);

### Pra quê?

- Você vai precisar do [Node.js][nodejs-download] por causa do Gulp;
- Você vai precisar do NPM para poder criar gerenciar os pacotes da sua aplicação(e instalar o Gulp);
- Você vai precisar od [Python][python-download] porque o NPM precisa do Python em certas circunstâncias.

___Lembre-se 1: eu não irei explicar cada tecnologia e nem ensinar como usa-las, apenas irei mostrar um exemplo de uma estrutura para o cotidiano.___

___Lembre-se 2: se você estiver no Windows você precisa adicionar o Node.js, o NPM e o Python nas variáveis de ambiente, [isso aqui deve ajudar](http://superuser.com/a/143121)___

### Por quê?

O que tava rolando na minha cabeça pra fazer esse tutô?

Mortes? Guerras? Caos? Destruição? Não dessa vez.

É simples: eu precisava de uma estrutura para poder trabalhar de forma _saudável_ em cima do __Angular.js__,
porque o __Angular.js__ carece muito de algumas caracteristicas que no caso
já são adotadas pelo __React.js__(falaremos sobre em outro post), eu também precisa de algo mais moderno, por isso a escolha do
[Babel][babeljs] e do [Browserify][browserify], e também queria ~~ser um hipster descolado e~~ automatizar tudo por isso escolhi o [Gulp][gulp].

<div style="text-align:center;">
  Pausa para procrastinar<br />
  <iframe width="560" height="315" src="https://www.youtube.com/embed/YEjQMMhDkjU" frameborder="0" allowfullscreen></iframe>
</div>

## Primeiros passos

Crie a seguinte estrutura de diretórios e arquivos, lembrando que se você quiser trocar o nome de alguma coisa, sinta-se a vontade, mas lembre de troca-los ao decorrer do tutô:

```text

src
'-- js
'   '-- config
'   '   '-- index.js
'   '   '-- boot.js
'   '-- controllers
'   '   '-- index.js
'   '   '-- home.js
'   '-- directives
'   '   '-- index.js
'   '   '-- video.js
'   '-- factories
'   '   '-- index.js
'   '-- resources
'   '   '-- index.js
'   '-- services
'   '   '-- index.js
'   '-- templates
'   '   '-- directives
'   '   '   '-- video.html
'   '   '-- index.html
'   '-- app.js
'-- less
'   '-- app.less
```

[javascript-doc]: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript
[angular-doc]: https://docs.angularjs.org/api
[browserify]: http://browserify.org/
[babeljs]: https://babeljs.io/
[gulp]: http://gulpjs.com/
[nodejs-download]: https://nodejs.org/
[python-download]: https://www.python.org/downloads/
[ramda-docs]: http://ramdajs.com/docs/
[less-docs]: http://lesscss.org/usage/