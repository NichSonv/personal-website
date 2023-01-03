---
title: "Espacializador circular"
listag: "-C"
date: 2022-12-23T09:20:56-03:00
draft: false
keywords: ""
weight: 0
hidden: false
---
# orbitAz.sc - Espacializador circular

OrbitAz é uma extensão que criei à biblioteca de classes do SuperCollider. Se trata de uma _pseudo-classe_, e sua principal função é trabalhar a espacialização de forma circular (especialmente perceptível em instalações sonoras com 3+ canais/amplificadores, em que o ouvinte consegue perceber nitidamente o som circulando ao redor).  
É uma funcionalidade que utilizei muitas vezes em minhas performances, especialmente com o instrumento [drone]({{< ref "drone" >}}).

## A extensão e sua documentação

{{< gist NichSonv 5ac344624ae85666962234f4656337ae orbitAz.sc >}}

{{< gist NichSonv 5ac344624ae85666962234f4656337ae orbitAz.schelp >}}

Pode-se observar no código que o efeito é resultado da junção do espacializador multicanal padrão - `PanAz` - com um envelope circular - `Env.circle`.  
O argumento principal em questão é o 'pan', do espacializador, e que controla a posição do som no espaço. A esse argumento é alimentado o envelope, que basicamente estará enviando um constante fluxo de dados entre 'min' e 'max'. Simplificadamente, o usuário define valores para 
- o número de canais utilizados (`numChans`);
- de "voltas" que o som vai dar (`cycles`);
- de quanto tempo em segundos cada volta vai durar (`time`);
- qual direção inicial o som vai girar (`dir`); e
- de qual ponto no espaço o som vai partir (`start`).