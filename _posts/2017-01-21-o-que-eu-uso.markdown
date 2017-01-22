---
title:  "Por que Scala, Go e PHP?"
date:   2015-09-07 10:18:00
description: Manual do programador ruim
---

Porque eu quero, vlw flw.

Calma, não vai ser tão fácil. Mas hoje vou deixar registrado porque eu em pleno
2017 ainda uso _PHP_, e por que Scala(não é trocadilho, sabemos que _PHP_ não escala,
não sem você fazer um pacto com alguma entidade DevOps antes).

# PHP

_PHP_, oh _PHP_. Linguagem odiada e amada por muitos, mas escrita de forma certa por
uma parcela ínfima de programadores. _PHP_ é uma linguagem fácil, e que se você
chutar uma pedra na rua voam 15 programadores _PHP_ prontos para aceitar um salário
de R$ 600,00, o que te da uma segurança de que o projeto que você fez vai poder
ser continuado caso acidentamente você morra(mas se você não for um bom programador
não vai adiantar de muita coisa). Entretanto, muito raro, muito raro mesmo,
alguém que saiba domar esse peixe-boi furioso, muitos ficam só no _Wordpress_ ou só
programam por cima, já que é isso que a linguagem prega: "programe pouco e saiba
menos ainda o que está programando". _PHP_ também prega um _deploy_ simples e sem
complicação(para o programador), mas é aí que mora o problema, no _PHP_ você não
tem controle sobre a _camada de rede_ da aplicação e ela fica toda a mercê do
servidor que você contratou, o que vai te forçar num futuro proximo, se você quiser
ter controle sobre sua aplicação a ter um servidor próprio, o que implica que
você vai ter que aprender a mexer no _Linux_,
instalar e configurar o _PHP_, _PHP-FPM_ e _Nginx_(ou se você for um pterodactylus do seculo passado, _Apache_)
só pra ter um __Hello World__ rodando no servidor, mas os problemas não terminam aí,
se seu conhecimento ainda for raso, você vai esbarrar no problema
**performance**, é, _PHP_ _in natura_ tem a pior performance, _PHP_ tem o pior
cuidado com os recursos do seu servidor, tão ruim que você poderia usar ele como
indice num medidor de performance de uma plataforma pra indicar o pior desempenho.
Mas, pra tudo existe uma solução, menos pro _PHP_, nem tanto, _PHP_ tem soluções boas,
apesar delas não eliminarem os problemas _naturais_ do PHP, tipo dizer que é uma
linguagem tipada(:joy: :joy: :joy:) e nem ao menos ter _Generics_ e até um tempo
atrás não saber que um _tipo_ pode ser `null`(sim, _PHP_ colocou type hinting de facto
no _5.6_, mas só descobriu que os tipos poderiam ser `null` no _7.1_, quase 4 anos depois, projetar pra quê?)
ou diferenciar uma _lista_ de um _dicionário_(_Lua_ também não consegue, mas ao menos _Lua_ tem _JIT_, chora _PHP_)[1],
_PHP_ possui algumas configurações super secretas como por exemplo o _OPCache_, que, basicamente
consiste em salvar todo código compilado num cache(vai vendo as gambiarras), acredite,
isso melhora MUITO o desempenho da aplicação e reduz drasticamente o uso de disco
do servidor, já que o _PHP_ lê e "compila" todos os arquivos da sua aplicação em
cada requisição(:joy:)[2], mas, isso não é uma optimização, porque o processamento
do código vai continuar sendo o mesmo, e é por isso que nosso caro querido amigo do peito,
Facebook, desenvolveu em seu laboratório o _Hack_, que basicamente optimiza
**de verdade™** o _PHP_ e dá a ele cara de uma linguagem decente, como o _Scala_ fez
com o _Java_, o _Hack_ surgiu da _HHVM_ e do _HipHop_(_HPHPc_), _HHVM_ é a VM do _Hack_, que é o compilador do
_PHP_ com _JIT_(aeeeeeeeeeeeeeeeeeeee) e que traz [muitas features ao PHP](https://docs.hhvm.com/hack/), _Hack_ é o santo graal do _PHP_, todo mundo já ouviu falar,
mas nunca usou, até porque, de todos os _frameworks_ famosos do _PHP_,
nenhum é compátivel 100% com o Hack porque [não querem seguir o padrão de código do Hack, que usa como base o PHP 5.6, já que o Hacke o PHP 7.1 possuem conflitos](http://hhvm.com/blog/875/wow-hhvm-is-fast-too-bad-it-doesnt-run-my-code),
sendo assim, no _PHP_ você escolher 2 caminhos: usar a _HHVM_ ou ter uma aplicação lixo, e a culpa nem vai ser sua :). Ah, já ia esquecendo, o Facebook pode indiretamente usar
_PHP_ em algumas áreas de sua stack, mas ele: 1 - faz 00 contribuição(es) para o PHP, visto que o Facebook utiliza Hack, 2 - usa Hack, 3 - usa HHVM, 4 - usa Hack e HHVM e não PHP.

# Go

Eu gosto do _Go_, é um gosto pessoal, apesar dele ser tão odiado por ser uma linguagem feia e totalmente alienigena,
ele apresenta uma otima performance e estábilidade(**de verdade™**) em _microserviços_(web e afins), não é a
linguagem mais fácil de se desenvolver porque sofre com o problema de versionamento de dependencias
no seu gerenciador de pacotes(mas temos ferramentas https://gopm.io/ e https://github.com/moovweb/gvm),
mas depois que você entende como funcionam os channels e a prototipagem, é uma ida sem volta(até porque só você no mundo vai conseguir dar manutenção nesse código).
_Go_ também é uma linguagem simples, sem muitas features e frescuras do mundo moderno da progração, mas diferente do _PHP_, não tenta inovar com coisas que deveriam ser no minimo uma obrigação de uma linguagem que ao menos quer ser chamada de projetada. É uma excelente escolha pra você que não quer programar _C_ e não quer chegar perto do _Javascript_ ou se aventurar no mundo obscuro do _Rust_(ainda vou fazer um post da minha aventura com _Rust_).

# Scala
Scala, agora sim uma linguagem e uma plataforma de verdade, você não conseguiria odiar ela(a menos
  que você utilize linguagens melhores que Scala, tipo Elixir), Scala tem pontos:
- SBT(Scala Build Tool, não é a emissora não), seu gerenciador de pacotes, que também é uma ferramenta de contrução de código
- Versionamento, SBT leva o versionamento a sério, ele utiliza o Ivy como resolvedor, e você além de poder utilizar multiplas versões
dos pacotes no mesmo ambiente de desenvolvimento, você pode usar multiplas versões dos pacotes na mesma aplicação, assim você não vai ter
conflito se quiser usar alguma coisa mais recente do que outra biblioteca que você usa, agora a cereja do bolo: VOCÊ PODE USAR MULTIPLAS
VERSÕES DO SCALA SEM TER 2 INSTALAÇÕES DO SCALA, é simples: O SBT roda no Scala instalado, mas o SBT pode também rodar a versão do SBT que
você preferiu referenciar na sua aplicação, e a sua aplicação pode rodar numa versão mais recente do Scala sem interferir no Scala já instalado,
isso acontece porque o Scala pode rodar o Scala, já que o compilador do Scala pode ser compilado com o Scala, e o compilador do Scala é nada mais, nada menos, que uma biblioteca, escrita em Scala(bootstraping yeah).
- Scala roda na JVM, Java é uma merda, sabemos disso, linguagem horrível, fundo do poço total, mas a JVM, a JVM representa, a JVM tem uma excelente
performance, é multi-core, possibilita threading, só consome um pouquinho de memória a mais, mas tudo tem seu preço, daí você pode dizer adeus
pra bibliotecas que precisam ser compiladas nativamente e essas coisas de plataformas fracas.
- Scala tem facilidades para paralelismo, aplicações orientadas a rede, Actor Model, Programação Reativa e Programação Funcional
- Scala tem Tipos **de verdade™**
- No Scala tudo é um objeto **de verdade™**
- Scala tem a melhor coisa que já descobri na minha vida, e não foi Scala, e sim [**PATTERN MATCHING**](http://docs.scala-lang.org/tutorials/tour/pattern-matching.html)(_Rust_ e _Elixir_ também possuem)

#### Scala tem bibliotecas, e bibliotecas pra todas as camadas da sua aplicação:
- [Rede com Actor Model](http://doc.akka.io/docs/akka/2.4/scala/index-network.html)
- [Serviços com Actor Model](http://doc.akka.io/docs/akka/2.4/scala/index-actors.html)
- [Clustering](http://doc.akka.io/docs/akka/2.4/scala/index-network.html)
- [Comunicação](http://doc.akka.io/docs/akka/2.4/scala/camel.html)
- [Dados](http://slick.lightbend.com/)

#### Scala tem frameworks, FUCKING FRAMEWORKS:
- [Play Framework](https://www.playframework.com/)
- [Spray](http://spray.io/) - hoje o Spray está sendo mergeado dentro do próprio Akka, e como você já percebeu, Akka é basicamente tudo no Scala.
- [Paralelismo](http://akka.io/)
- [Actor Model](http://akka.io/) - Mais Akka
- [Scalatra](http://www.scalatra.org/) - pra você que amou Ruby
- [Functional Relation Mapping](http://slick.lightbend.com/) - ORM é coisa do passado

#### Scala tem features:
- [Pattern Matching](http://docs.scala-lang.org/tutorials/tour/pattern-matching.html)
- [Promises e Futures](http://docs.scala-lang.org/overviews/core/futures.html)
- Operator overloading, porque você programar deve ser mais dificil ainda:
{% highlight scala %}
class Useless {
  def +(other: Int) = other + 1
}
{% endhighlight %}
- [Macros](http://docs.scala-lang.org/overviews/macros/overview.html)
- Reflections feitas do jeito certo com reflexões feitas em tempo de compilação e não em runtime(você também pode fazer reflections em runtime se precisar :wink:)
- Metaprogramação

#### Scala não tem:
- Case classes aplicáveies e deplicáveis(apply e unapply com tuplas) com mais de 22 atributos :( mas isso vem sendo consertado com [Shapeless e programação generica](https://github.com/milessabin/shapeless)
- Uma forma de acabar com o Type Erasure da JVM de forma amigável sem fazer você escrever umas 2 linhas de código a mais

--------------------

É isso aí, não recebi nenhuma grana da LightBend pra fazer propaganda do Akka e do Slick, não posso fazer nada se ela tem de tudo. Também não recebi grana do Martin Odersky.

--------------------

- [1] Você pode optmizar a verificação pra saber se um `array` é uma _lista_ ou _dicionario_ encapsulando o array e usando [isso](http://php.net/manual/en/class.cachingiterator.php) ;)
- [2] Se você é um programador ao menos decentezinho que usa composer, o composer costuma literalmente foder com o desempenho da sua aplicação porque ele faz muitas requisições ao disco, então habilitar o OPCache vai fazer sua aplicação ser menos pior.
