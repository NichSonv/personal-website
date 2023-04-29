---
title: "Prime-number-gen.sc"
desc: "Algoritmo gerador de arrays de números primos - ext. SC"
date: 2022-12-23T09:41:36-03:00
draft: false
keywords: ""
weight: 0
hidden: false
type: portfolio
---
# Gerador de números primos

Essa é uma extensão que programei para o SuperCollider, se trata de um método de criação de listas, que preenche uma lista somente com números primos, e seus únicos dois argumentos são o tamanho da lista, e o número de partida.

{{< gist NichSonv 588686251461f040d9ee985a5932afe1 00_Prime-number-gen.sc >}}

E essa aqui é a versão anterior, antes de eu descobrir que existia um método nativo que identifica se um número é primo ou não...

{{< gist NichSonv 588686251461f040d9ee985a5932afe1 01_Prime-number-gen-V1.scd >}}

Basicamente, o algoritmo cria uma lista de `nil`'s, de acordo com o `size` determinado, depois roda um loop `while` para cada elemento, em ordem crescente de _index_, adicionando os números primos em ordem crescente a partir do `start`.  
Para saber se é primo ou não, o algoritmo checa cada número inteiro, em sequência, desde `start`, utilizando o método nativo `.isPrime`, que retorna um _bool_ `true` ou `false`.

No segundo caso, que não utiliza o método `.isPrime`, o algoritmo divide o inteiro que está conferindo por todos os inteiros, de 1 até o atual, e guarda todos os resultados (agora _floats_) em uma segunda lista, temporária, onde depois vai transformá-los em _strings_, separar tudo que está à esquerda do "." com o que está à direita (decimais) - o que vai tornar cada string em uma sub-lista de dois strings -, e então, ele busca dentre todos os strings resultantes os que são `"0"`, e para cada um que encontra, soma à um contador. Se esse contador no final resultar num total de `2`, significa que o número é primo, pois só foi dividido exatamente por 1 e por ele mesmo.

```sclang
// Divide o inteiro por todos os inteiros de 1 até ele, e salva na lista 'temp'.
temp = count/(1..count);

// Transforma todos os floats em strings e os divide em dois elementos, apagando o '.'
temp = temp.collect{
	| n |
	n = n.asString;
	n.split($.);
};

// Confere a nova lista em busca de "0"s, e adiciona ao contador
temp.deepCollect(2) {
	| n |
	if(n=="0") {check = check + 1; check.postln}
};

// Confere se é primo ou não
if(check==2) {prime=true}
```