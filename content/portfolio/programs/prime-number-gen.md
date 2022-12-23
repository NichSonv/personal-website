---
title: "Gerador de nºs primos"
listag: "-C"
date: 2022-12-23T09:41:36-03:00
draft: false
keywords: ""
weight: 0
hidden: false
---
# Gerador de números primos

Essa é uma extensão que programei para o SuperCollider, se trata de um método de criação de listas, que preenche uma lista somente com números primos, e seus únicos dois argumentos são o tamanho da lista, e o número de partida.

{{< gist NichSonv 588686251461f040d9ee985a5932afe1 00_Prime-number-gen.sc >}}

E essa aqui é a versão anterior, antes de eu descobrir que existia um método nativo que identifica se um número é primo ou não...

{{< gist NichSonv 588686251461f040d9ee985a5932afe1 01_Prime-number-gen-V1.scd >}}