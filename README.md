<p align="center">
  <img src="https://img.shields.io/static/v1?label=SpringExpert - Dev Superior&message=Testes Automatizados&color=8257E5&labelColor=000000" alt="Testes automatizados na prática com Spring Boot" />
</p>

# Tópicos

# Parte teórica

[Tipos de teste](#tipos-de-teste)
-
- [Teste unitário](#teste-unitário)
- [Teste de integração](#teste-de-integração)
- [Teste funcional](#teste-funcional)

[Benefícios de testes automatizados](#benefícios-de-testes-automizados)
-
- [Detecção de mudanças](#1-detecta-facilmente-se-mudanças-violam-regras-do-sistema)
- [Forma de documentação](#2-é-uma-forma-de-documentação)
- [Redução de custos](#3-redução-de-custos)
- [Melhor design](#4-melhora-design-da-solução)

[TDD - Teste Driven Development](#o-que-é-tdd---test-driven-development)
-
- [Princípios e vantagens](#princípios--vantagens)
- [Como fazer](#processo-básico)

[Boas práticas para testes](#boas-práticas-para-testes)
-
- [Nomeclatura](#nomeclatura-de-um-teste)
- [Padrão AAA](#padrão-aaa)
- [Princípios inversão de dependência](#princípio-inversão-de-dependência-solid)
- [Independência e isolamento](#independência-e-isolamento)
- [Cenário único](#cenário-único)
- [Previsibilidade](#previsibilidade)
<hr>

# Parte prática

[Visão geral JUnit](#visão-gerão-junit5)
-
- [Utilizando Factory para instanciar objeto](#padrão-de-projeto-factory-para-instanciar-objetos)
- [Primeiro teste na prática](#primeiro-teste-na-prática-com-junit)
- [Testando método deposit](#testando-se-o-método-deposit-está-realmente-depositando-e-descontando-a-taxa)
- [Testando deposit com quantia negativa](#testando-se-o-método-deposit-não-faz-nada-com-quantia-negativa)
- [Teste full withdraw](#teste-saque-total)
- [Teste withdraw](#teste-saque)
  - [Saldo positivo](#saque-com-saldo-positivo-maior-que-o-saque)
  - [Saldo negativo (com exceção)](#saque-com-saldo-insuficiente-exception)
- [Observação TDD](#observação-tdd)

# Objetivo

# UML

## Tipos de teste

Existem outros tipos de testes, mas abaixo falaremos dos mais comuns.

### Teste Unitário

É um teste feito pelo desenvolvedor, ele valida comportamento de **unidades funcionais de código**. Ou seja: testa os
métodos de uma classe.

Um teste unitário **NÃO** pode acessar outros componentes ou recursos externos (arquivos, bd, rede, web services, etc.).

Portanto, se estamos fazendo um teste unitário de um controlador, não podemos instanciar um Service/Repository e nem
acessar banco, rede, nem nada do tipo.

A ideia é que a gente instancie um "mock", um objeto de "mentirinha" para simular o comportamento do objeto dependente,
testando a UNIDADE de forma ISOLADA.

### Teste de Integração

Agora sim! Testamos a comunicação entre componentes e modulos da aplicação (e também recursos externos), verificando se
estão interagindo entre si corretamente.

### Teste Funcional

Um teste do ponto de vista do usuário. Se uma determinada funcionalidade está executando corretamente, produzindo o
resultado ou comportamento desejado pelo usuário (**casos de uso, por exemplo**).

## Benefícios de testes automizados

### 1. Detecta facilmente se mudanças violam regras do sistema

Quando atualizarmos algo no sistema, mudar alguma implementação apertaremos um botão! E esses testes irão rodar, 
verificando se alguma coisa violou as regras da aplicação.

### 2. É uma forma de documentação

Lendo a documentação do teste, ele registra o comportamento, ou seja, nos informa como o teste deve se comportar
(entrada e saídas esperadas), se deverá gerar uma exceção, etc. 

### 3. Redução de custos

Se fizermos alguma manutenção no sistema e ele possuir, estiver coberto de vários testes automizados, será muito mais
fácil validar a manutenção (o que geralmente é bem caro).

### 4. Melhora design da solução

Uma aplicação testável precisa ser bem desenhada e projetada.

## O que é TDD - Test Driven Development

É um **metodo** de desenvolver software. Considere um desenvolvimento guiado pelos testes. Não é porque seu software
possui testes automatizados que ele é TDD.

### Princípios / vantagens:

- Foco nos requisitos (iniciar o projeto escrevendo os testes primeiro)
- Tende a melhorar design do código, pois o código deverá ser testável
- Acréscimos no projeto têm menos chance de quebrar a aplicação (passar nos testes)

### Processo básico:

1. Escreva o teste como esperado (naturalmente que ele ainda estará falhando)
2. Implemente o código necessário para que o teste passe
3. Refatore o código conforme for necessário

## Boas práticas para testes

### Nomeclatura de um teste

``<AÇÂO> should <EFEITO> [when <CENARIO>]``

Leia-se exemplo: ``<método delete> SHOULD <deletar objeto> [<when ID existir>]``

### Padrão AAA

- Arrange: instancie os objetos necessários (um New ou algo do tipo)
- Act: execute as ações necessárias (deletar, inserir algo/regra de negócio)
- Assert: declare o que deveria acontecer (resultado esperado)

### Princípio inversão de dependência (SOLID)

Se uma classe A depende de uma instância da classe B, não tem como testar a classe A de forma isolada. Na verdade, nem
seria um teste unitário. Por isso utilizamos o AutoWired ou construtores.

A inversão de controle ajuda na testabilidade e garante o isolamento da unidade a ser testada. Ou seja, ao invés de
instanciarmos a classe B, instanciaremos o **Mock**, o objeto de "mentirinha" que simulará o **comportamento** da classe B.

### Independência e isolamento

Um teste não pode depender de outros testes, nem da ordem de execução.

### Cenário único

- O teste deve ter uma lógica simples, linear
- O teste deve testar apenas um cenário
  - Igual o exemplo acima. Se você faz um teste para deletar um ID existente, deve existir OUTRO teste para deletar com
  um ID não existente
- Não use condicionais e loops

### Previsibilidade

O resultado do teste deve ser sempre o mesmo para os mesmos dados.

Ou seja, não é uma boa fazer o resultado do teste depender de algo que pode variar (tipo timestamp atual (Instant.now()))
e valores aleatórios.

## Visão gerão Junit5

### [Site](https://junit.org/junit5/)

1. Criar uma classe de testes
2. A classe pode conter um ou mais métodos com a annotation @Test
3. Um método de @Test deve ser void
4. O objetivo é que todos os métodos @Test passem sem falhas
5. O que define se um método @Test passa ou não são as "assertions" deste método
6. Se um ou mais falhas ocorrem, estão são mostradas depois da execução do teste

## Primeiro teste na prática com JUnit

Inicialmente já sabemos que na nossa aplicação Spring é criado automaticamente um pacote "test". Assim sendo, se formos
testar uma entidade, criar um pacote entities, se for repository uma de respositoy e assim vai...

No exemplo abaixo é uma aplicação sem Spring ou ela possui uma classe Account com atributo Id e balance + getters e
setters e métodos de: deposit, withdraw e fullWithdraw:

![img.png](img.png)

![img_1.png](img_1.png)

No pacote test > entities: criar "AccountTests" onde ficará todos os testes pertinentes a essa entidade.

### Testando se o método deposit está realmente depositando e descontando a taxa

Agora aplicamos tudo da parte prática.

A nomeclatura sendo: o nome do método + "should" + efeito do método + cenario

E o padrão AAA: instanciando o objeto, executando a ação e depois aferindo o resultado.

![img_2.png](img_2.png)

### Testando se o método deposit não faz nada com quantia negativa

Tentando depositar uma quantia negativa.

Instanciamos a conta com um valor esperado. Ao realizar o depósito negativo, o valor deve continuar o mesmo.

![img_3.png](img_3.png)

### Teste saque total

Deve limpar o saldo e retornar todo o saldo.

Temos dois assertions porque:

O primeiro: testa se o valor que a gente espera de fato é zero.

O segundo: testa para ver se o retorno (o que foi sacado) é igual ao balanço inicial.

![img_7.png](img_7.png)

### Teste saque

Um cenário onde a quantia que queremos sacar está ok! E outro quando a quantia que queremos sacar é superior ao saldo
onde terá uma exception.

#### Saque com saldo positivo (maior que o saque)

![img_8.png](img_8.png)

#### Saque com saldo insuficiente (exception)

Agora não será somente assertTrue ou That e sim **Throws, em virtude da exception!**

E o AA ficará dentro de uma expressão lambda, veja:

![img_9.png](img_9.png)

## Padrão de projeto Factory para instanciar objetos

O ideal é que tenhamos uma classe para instanciar objetos para gente (caso seja uma operação repetitiva no sistema).

No pacote testes criar um pacote factory. Como a classe é Account se chamará **AccountFactory**. Criaremos um método
para instanciar uma Account vazia (esses métodos geralmente são estáticos).

![img_4.png](img_4.png)

Como visto acima, pode ser até mesmo **uma classe com um valor pré-definido**.

Agora dentro dos testes, ao invés de instanciar um new Account, utilizaremos a factory.

![img_5.png](img_5.png)

![img_6.png](img_6.png)

## Observação TDD

O que fizemos acima, não foi TDD. Seria somente se tivéssemos criado no máximo a classe Account sem os métodos, somente
atributos com getters e setters.

O ideal seria criar a classe de Testes, exatamente como está ali em cima depois implementar os métodos.

## Exercício JUnit vanilla