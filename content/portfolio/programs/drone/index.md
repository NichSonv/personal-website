---
title: "Drone.scd"
desc: "Instrumento virtual e interface"
date: 2022-12-17T22:49:17-03:00
draft: false
keywords: "-, nicholas, sonvezzo, somvezzo, som-vezzo, -"
weight: 0
hidden: false
---
# {{< param title >}} - {{< param desc >}}

{{< gist NichSonv "1d0501e682b0f6be6268408d43cf48da" "drone.scd" >}}

O instrumento virtual `\drone` se trata de um sintetizador que programei em SuperCollider (_sclang_), e que se aproveita do efeito acústico das _formantes_, ou frequências de ressonância - simplificadamente, a ênfase de algum harmônico dentro de um som complexo.  
A principal classe em sua construção, e que é a base da sua sonoridade, é a `Formant.ar`, que como o nome sugere, cria esse som complexo onde é possível definir a _formante_, e também o tamanho da banda de ressonância. O instrumento utiliza esse oscilador em conjunto com um reverb e controle de espacialização, e aí está criada a sua sonoridade característica.

```sclang
SynthDef(\drone, {
    | sig env | // argumentos
    env = Env.asr.kr(2, \gate.kr(1)); // envelope para a duração do som (asr = Attack Sustain Release)
    sig = Formant.ar(\fundamental.kr(200), \formante.kr(800), \banda.kr(1000), env); // oscilador base do instrumento
    sig = Pan2.ar(sig, \pan.kr(0)); // espacializador
    sig = FreeVerb.ar(sig, \mix.kr, \room.kr, \damp.kr); // reverb (normalmente adicionado de forma externa ao instrumento)
    Out.ar(0, sig) // canal de saída do som para a placa de áudio
}).add;
```

O instrumento normalmente é utilizado com a ajuda de uma interface digital, que também criei especificamente para ele, através do programa _TouchOSC_, abaixo a imagem de uma das versões dessa interface, desenhada para uso em um iPad.

{{< figure src="drone-controls1.png" link="drone-controls1.png" >}}

Talvez possa parecer complicado, mas isso é só pelo fato dessa interface, em particular, permitir seis instâncias do instrumento ao mesmo tempo. Basicamente, possui controles de ON/OFF, volume, frequência, espacialização, reverb, abertura de banda, formante e a opção de salvar ou carregar as mais diversas combinações dessas configurações.

A comunicação do aparelho ao SuperCollider foi em OSC nas primeiras versões, dentro de uma rede wifi fechada apenas para os aparelhos envolvidos na performance, e mais recentemente em MIDI, pela vantagem da comunicação poder ser feita através de um cabo USB, com isso diminuindo a possibilidade de _lag_.

Abaixo um exemplo do instrumento em prática, em uma versão da obra [Atmosphere]({{< ref "atmosphere.md" >}}) (ouça com fones de ouvido para uma melhor experiência):

{{< soundcloud src="1036050955" href="atmosphere" title="Atmosphere" >}}