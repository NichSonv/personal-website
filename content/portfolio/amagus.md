---
title: "Âmagus project"
subhead: "Compositor • Programador"
date: 2022-12-12T14:30:22-03:00
draft: true
keywords: "-, nicholas, sonvezzo, somvezzo, som-vezzo, -"
weight: 0
hidden: true
---
# Âmagus

## O que é?

Âmagus foi o meu projeto de final de curso, do bacharelado em composição musical na Unicamp. Se trata de uma peça autoral _live-eletronics_ (em suma, uma música que mistura sons acústicos e digitais - processamento de áudio, síntese sonora...). É um ambiente de improvisação e processos estocásticos que seguem certas diretrizes, programado em _sclang_, no SuperCollider.

## Interface e programação

<a href="/amagus/amagus1.png"><img src="{{ relref . "amagus1.png" }}></a>

Essa foi uma interface que criei para a execução da peça Âmagus, em julho/2022 ([link para gravação no YT](https://youtu.be/Ey08N9ciDtE)). Todo o design, comportamento dos botões, páginas etc, foi feito através do programa _TouchOSC_, e todo o código que programa as ações dos mesmos, foi escrito em _sclang_, no _SuperCollider_, que também é onde tudo é processado.

<!-- ![amagus1](amagus1.png) Why isn't it working... -->

A primeira página possui cinco botões, cada um correspondente a um _movimento_ da peça, ou em termos de programação, uma função pré-definida. Cada botão inicializa o próximo estágio, configurando variáveis novas, 

<!-- {{< gist >}} -->
