---
title:  "Banco de dados mil grau"
date:   2015-09-30 10:18:00
description: Como eu organizo meus bancos de dados para evitar que o caos se instale
---

Neste meu primeiro e breve post irei mostrar como eu organizo meus bancos de dados para evitar que o caos se instale e mate pessoas.

A ideia é simples: __KEEP IT SIMPLE__. Não, não tem __STUPID__, porque o padrão é meu, se você não usa, de boa, seja feliz, é _nóis_.

Suponhamos que você possua uma _data layer_ na sua aplicação, essa _data layer_ possui seus modelos de dados, que por sua vez é singular porque modelo é singular, trata-se de só 1(HUM) e unico modelo, logo o nome de nossos modelos será _SINGULAR_, exemplos:


```

Usuario
'-- Perfil

```

_Detalhe que acima vai depedender muito do seu coding style, mas lembre-se de manter tudo no_ ___singular___ _._


No DB temos as tabelas, já que cada tabela irá armazenar ___n___ informações geradas por um unico modelo o nome da tabela há de ser _PLURAL_, usando _snake case_ e tudo minusculo sem acentos ou abreviações ou prefixos, just keep it simple. Exemplos:

```
usuarios
usuario_perfis
```

Agora algo interessante: cada usuário possui um perfil, a tabela __usuario_perfis__ armazena ___n___ perfis, então tenho __usuario__ e __perfis__, formando __usuario_perfis__, se fosse uma tabela __n → n__, você teria __usuarios_musicas__ e em casos de relação __1 → 1__ teriamos __usuario_perfil__, entendeu o ponto? Isso serve para não se confundir, se você tem a tabela nomeada como __usuario_perfis__ você já sabe de cara que ela é __1 → n__, lembrando sempre de manter quem manda na relação na esquerda e quem depende da relação na direita, no caso de __n → n__ matenha o mais importante na esquerda.

__É TERMINANTEMENTE OBRIGATÓRIO__ que cada tabela tenha uma coluna __id__, não, não venha com __CD__, não venha com **ID_USARIO**, **INT\_ID\_USUARIO**, **PK_USUARIO**, não. É __id__ e ponto. Jamais case algum indice com o id(dual primary key), __JAMAIS__, o __id__ é unico e não pode ter nenhum outro igual em circunstância alguma, nem com forças divinas, praticamente todos os frameworks de _data layer_ usam essa regra e quebrar regras vai fazer com que seu código fique massivo e cheio de configurações inúteis.

Em casos de campos entrangeiros tenho o seguinte: na tabela __usuario\_perfis__ teremos o campo __usuario\_id__, que refere a um unico __usuario__, claramente na tabela __usuarios__, identificado pela coluna __id__, não é simples? É simples sim.

Em casos de campos estrangeiros __n → n__ tenho o seguinte: teriámos a tabela __musicas__, a tabela __usuarios__, e ambas se relacionam usando a tabela __usuarios\_musicas__ como pivô, formando essa estrutura:

```
musicas
'-- id
'-- ...

usuarios
'-- id
'-- ...

musicas_usuarios
'-- id
'-- usuario_id
'-- musica_id
```

Essa é a minha lógica ao nomear coisas relacionadas ao banco de dados. Existem pessoas que gostam de usar singular em tudo e eu não vejo problemas nisso, em alguns projetos que não envolvem _data layer_ eu costumo usar singular também.

### Algumas regrinhas basicas :)


Regra 0: evite qualquer tipo de prefixo, seja tbl, tabela, table, t, amiguinho, batata, abacate, etc. definitivamente não use prefixos, nem no nome da tabela, nem no nome das colunas, prefixos são feios e não são nada _aesthetic_.;

Regra 1: evite ter mais de 20 campos numa tabela, sim, 20 campos, se você pegasse seu RG e colocasse todas as suas informações nele, tipo CNH, CPF, numero do cartão de crédito, comprovante de residência, certidão de nascimento, informações da CLT, nome de seus irmãos, pais, tipo sanguíneo e titulo de eleitor, ficaria ridiculo, não? Massivo? Feio? Não seria nada prazeroso procurar uma informação nele, não é? Pois é, nossas tabelas também são assim, quanto mais colunas mais arduo é o trabalho de manusear e entender a semantica dos dados;

Regra 2: generalize os dados: celular e telefone são numero telefones, devem estar numa tabela __usuario_telefones__ organizados por tipos, e não como coluna na tabela usuários. Isso também serve para endereço, e-mail, documentos, etc.;

Regra 3: Lembre-se de que um dia sua aplicação pode chegar numa escala internacional e que isso pode acarretar sérios problemas caso você tenha deixado sua tabela recheada de colunas contendo dados locais tipo CPF, RG, CEP, CNH, etc., localize seu DB também! Crie uma tabela __usuario\_documentos__, organize cada documento por tipo, seja feliz!;

Regra 4: no nome da tabela e das colunas somente letras e/ou underline, nada de numeros ou simbolos;

Regra 5: nd de abbr nomes.


Adendo sobre a regra 2: "AH, mas isso vai complicar as query tudo :(", será?

```sql
SELECT
  d.*
FROM 
  usuario_documentos d 
WHERE 
  d.usuario_id = 1 
  AND d.tipo = /*<flag do tipo do documento, provida pela data layer ou um enum no db>*/;
```


É isso. vlw flw.