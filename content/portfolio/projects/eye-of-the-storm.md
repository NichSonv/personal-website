---
title: "Eye of the Storm"
desc: "Composição em sclang"
date: 2022-12-15T13:33:16-03:00
draft: false
keywords: "-, nicholas, sonvezzo, somvezzo, som-vezzo, -"
weight: 0
hidden: false
---
# Eye of the Storm - WIP

Ouça com fones de ouvido e um volume moderado:

{{< soundcloud src="1104087820" href="eots-demo" title="Eye of the Storm (demo)" >}}

Essa demo foi programada e gravada no SuperCollider, e é composta por alguns sintetizadores e sequenciadores...

_"WaveBass"_  
```sclang
~buf = Buffer.alloc(s, 2048*4);

~bass_wt = Env(
    [0] ++ ( {rrand(-0.95, 0.95)} !14) ++ [0],
    ( {rrand(0.01, 15.0)} !15 ),
    ( {rrand(-12.0, 12.0)} !15 )
).asSignal(1024*4).asWavetable;
~buf.loadCollection(~bass_wt);

SynthDef(\waveBass, {
    | sig env |
    env = EnvGen.kr(Env.asr(\atk.kr(0.1), \amp.kr(0.5), \rel.kr(1)), \gate.kr(1), doneAction: 2);
    sig = Osc.ar(~buf, \freq.kr(100, 0.4)*[1, 2.01], 0, env);
    sig = LeakDC.ar(sig);
    sig = Splay.ar(sig, \spr.kr(0.2, 0.2), 1, \pan.kr(0, 0.2));
    sig = sig * 0.4;
    Out.ar(\out.kr(0), sig)
}).add;
```

_"Hi-hat"_  
```sclang
SynthDef(\click, {
    | sig env |
    env = EnvGen.kr(Env.perc(0.01, \rel.kr(0.1), \amp.kr(1)), doneAction: 2);
    sig = WhiteNoise.ar(env!2);
    sig = Balance2.ar(sig[0], sig[1], \pan.kr(0, 0.2), 0.5);
    Out.ar(\out.kr(0), sig)
}).add;
```

## Origem do projeto - trilha alternativa

Antes de se tornar uma música independente, a obra era parte de um projeto coletivo de graduação, feito no 1º semestre de 2020; um exercício de criação de trilha sonora alternativa para um curta ou trecho de filme existente. Nesse caso, o curta em questão pode ser encontrado [aqui](https://www.youtube.com/watch?v=H1mX8ptsmBM), de onde extraímos o vídeo, recriamos toda a sonoplastia, e então a composição da nova trilha.
