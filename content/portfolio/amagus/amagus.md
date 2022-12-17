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

Âmagus foi o meu projeto de final de curso, do bacharelado em composição musical na Unicamp. Se trata de uma peça autoral _live-eletronics_ (isto é, uma música que mistura sons acústicos com processos em um computador, como processamento de áudio, síntese sonora, execução de funções, código...). É um ambiente de improvisação e processos estocásticos que seguem certas diretrizes, programado em _sclang_, no SuperCollider.

## Interface e programação

Essa foi uma interface que criei para a execução da peça Âmagus, em julho/2022 ([link para gravação no YT](https://youtu.be/Ey08N9ciDtE)). Todo o design, comportamento dos botões, páginas etc, foi feito através do programa _TouchOSC_, e todo o código que programa as ações dos mesmos, foi escrito em _sclang_, no _SuperCollider_, que também é onde tudo é processado.

{{< figure src="/portfolio/amagus/amagus1.png" link="/portfolio/amagus/amagus1.png" >}}

A primeira página possui cinco botões, cada um correspondente a um _movimento_ da peça, ou em termos de programação, uma função pré-definida. Apertar um botão significa encerrar os processos da função anterior, preparar o ambiente e iniciar os processos da nova função (movimento) - abaixo um exemplo de uma dessas funções no código:

{{< gist NichSonv a7084ba76b8726f984920a4f5ffaec2e "etheriumf.scd" >}}