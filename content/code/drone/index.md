---
title: "Drone"
desc: "Sintetizador"
date: 2022-12-17T22:49:17-03:00
draft: false
keywords: "-, nicholas, sonvezzo, somvezzo, som-vezzo, -"
weight: 0
hidden: false
type: portfolio
---
# {{< param title >}} - {{< param desc >}}

{{< gist NichSonv "1d0501e682b0f6be6268408d43cf48da" "drone.scd" >}}

`\drone` é um sintetizador que programei em SuperCollider (_sclang_). Sua sonoridade remete à um metal sendo friccionado com um arco.

_Exemplo da sonoridade do sintetizador..._
{{< soundcloud src="1036050955" href="atmosphere" title="Atmosphere" >}}

---

```sclang
Formant.ar(fundFreq, formant, bandwidth, mul)
```

A classe acima é a que instancia o oscilador principal do synth, que gera o seu som característico.

- `Formant` - a classe
- `.ar` - o método para instanciar um oscilador em taxa de áudio
- `fundFreq` - parâmetro que controla a frequência base do oscilador
- `formant` - parâmetro que controla a frequência do harmônico
- `bandwidth` - parâmetro que controla a abertura de banda do filtro
- `mul` - parâmetro que multiplica a amplitude do sinal

No todo, o sintetizador é bem simples, a `Formant` cria um sinal em taxa de áudio, o `Env` cria o envelope que vai determinar os níveis desse sinal so longo do tempo, o `PanAz` espacializa o sinal, o `Splay` reduz o espaço sonoro para um ambiente stereo (quando necessário, pois o instrumento foi pensado para atuar, principalmente, em instalações sonoras de 3+ caixas de som), `LeakDC` re-centraliza as amplitudes do sinal entre -1 e 1, para caso ele acabe pendendo demais para um dos dois lados, e `Out` envia o sinal para fora (seja a caixa de som ou algum bus interno).  
Depois disso tudo, o sinal ainda passa por um reverb, que é fundamental também para que o som característico do synth surja.

O instrumento normalmente é utilizado com a ajuda de uma interface digital, que também criei especificamente para ele, através do programa _TouchOSC_, abaixo a imagem de uma das versões dessa interface, desenhada para uso em um iPad.

{{< figure src="drone-controls1.png" link="drone-controls1.png" >}}

Talvez possa parecer complicado, mas isso é só pelo fato dessa interface, em particular, permitir seis instâncias do instrumento ao mesmo tempo. Basicamente, possui controles de ON/OFF, volume, frequência, espacialização, reverb, abertura de banda, formante e a opção de salvar ou carregar as mais diversas combinações dessas configurações.

A comunicação do aparelho ao SuperCollider foi em OSC nas primeiras versões, dentro de uma rede wifi fechada apenas para os aparelhos envolvidos na performance, e mais recentemente em MIDI, pela vantagem da comunicação poder ser feita através de um cabo USB, com isso diminuindo a possibilidade de _lag_.

Abaixo um exemplo do instrumento em prática, em uma versão da obra [Atmosphere]({{< ref "atmosphere.md" >}}) (ouça com fones de ouvido para uma melhor experiência):
