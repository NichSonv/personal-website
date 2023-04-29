---
title: "Âmagus"
desc: "Recital de formatura"
date: 2022-12-12T14:30:22-03:00
draft: false
keywords: "-, nicholas, sonvezzo, somvezzo, som-vezzo, -"
weight: 0
hidden: false
type: portfolio
---
# Âmagus

## O que é?

{{< video src="https://youtube.com/embed/Ey08N9ciDtE" title="amagus" >}}

Âmagus foi o meu TCC de bacharelado em composição musical na Unicamp.  
Se trata de uma peça autoral _live-eletronics_ (isto é, uma música que mistura sons acústicos com processos em um computador, como processamento de áudio, síntese sonora, execução de funções, código...). É um ambiente de improvisação e processos estocásticos que seguem certas diretrizes, programado em _sclang_, no SuperCollider.

## Interface e programação

Essa foi a interface que criei para a execução da peça. Todo o design, comportamento dos botões, páginas etc, foi feito através do programa _TouchOSC_, e todo o código que programa as ações dos mesmos, foi escrito em _sclang_, no _SuperCollider_, que também é onde tudo é processado.

### Interface página 1 - Globais

{{< figure src="amagus1.png" link="amagus1.png" >}}

{{< gist NichSonv "a7084ba76b8726f984920a4f5ffaec2e" "00_midiGlobals.scd" >}}

A primeira página possui cinco botões, cada um correspondente a um _movimento_ da peça, ou, na programação, uma função pré-definida. Apertar um botão significa encerrar os processos da função anterior, preparar o ambiente e iniciar os processos da nova função (movimento).  
Além dos cinco botões principais, há um sexto, pequeno, para a eventual necessidade de desligar todos os processos, em uma emergência. O famoso "botão do pânico".

### Interface página 2 - Sequenciadores

{{< figure src="amagus2.png" link="amagus2.png" >}}

{{< gist NichSonv "a7084ba76b8726f984920a4f5ffaec2e" "01_primalsMidi.scd" >}}

A segunda página consiste em uma matrix/tabela 7x3, onde cada coluna corresponde à um sequenciador, e cada fileira, enfatizada pelas cores, uma ação àquele sequenciador. Cada sequenciador, do 1 ao 7, aumenta em quantidade o número de sons por segundo, e todos distribuem o tempo entre cada som (silêncio) de forma aleatória, o que gera sempre um ritmo diferente a cada iteração.  
Para os respectivos sequenciadores, os botões verdes inicializam a sequência, os azuis re-iteram a aleatoriedade dos silêncios, e os vermelhos encerram a sequência.

### Interface página 3 - \drone

{{< figure src="amagus3.png" link="amagus3.png" >}}

{{< gist NichSonv "a7084ba76b8726f984920a4f5ffaec2e" "02_spectrumMidi.scd" >}}

A página três contêm uma versão reduzida e atualizada dos controles para o instrumento virtual _[Drone]({{< ref "drone.md" >}})_, possibilitando até três instâncias simultâneas do instrumento, com controles separados de espacialização, volume, reverb, delay, tremolo, on/off, e o mais importante, controles X/Y para controlar o timbre e formante principal do instrumento, que são suas características mais essenciais.

## Sobre a peça e execução

A poética por detrás da composição na verdade é muito simples, foi uma junção das principais vertentes com as quais gosto de trabalhar dentro da área musical, e isso pode ser observado nos cinco movimentos da peça:

1. _"Etherium"_ - Música coral / Música sacra;
2. _"Anima"_ - Violão e sons acústicos;
3. _"Primals"_ - Síntese sonora e sequenciadores;
4. _"Memoria"_ - Processos eletroacústicos e processamento de áudio;
5. _"Spectrum"_ - Música meditativa.

<p class="centered"><strong>
Você pode analisar o código completo clicando <a target="_blank" href="https://github.com/NichSonv/compositions/blob/abd53d6ad0e959b7159114f08dc05bce09b3e79d/amagus.scd">aqui</a>
</strong></p>
<!-- 
planejamento conteúdo:
- Resumo do que é 
- Interface e programação
- Sobre a peça - poética e execução
-->