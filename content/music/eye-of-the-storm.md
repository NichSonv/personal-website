---
title: "Eye of the Storm"
desc: "Composição em sclang"
date: 2022-12-15T13:33:16-03:00
draft: false
keywords: "-, nicholas, sonvezzo, somvezzo, som-vezzo, -"
weight: 0
hidden: false
type: portfolio
---
# Eye of the Storm - WIP

Ouça com fones de ouvido e um volume moderado:

{{< soundcloud src="1104087820" href="eots-demo" title="Eye of the Storm (demo)" >}}

Essa demo foi programada e gravada no SuperCollider, e é composta por alguns sintetizadores e sequenciadores...

## Baixo

O baixo é o primeiro som que se escuta na música, e ele é basicamente composto por dois sintetizadores tocando junto, um gerador de ruído branco com filtro passa-banda, e o oscilador que gera as notas de fato, cujo formato de onda é criado com a técnica de _waveshaping_.

```sclang
// Sintetizadores e wavetable
~buf = Buffer.alloc(s, 2048*4);
~bass_wt = Env(
    [0] ++ ( {rrand(-0.95, 0.95)} !14) ++ [0],
    ( {rrand(0.01, 15.0)} !15 ),
    ( {rrand(-12.0, 12.0)} !15 )
).asSignal(1024*4).asWavetable;
~buf.loadCollection(~bass_wt);

SynthDef(\vent, {
    | sig env opn den |
    den = ExpRand(1e4, 1e5);
    opn = \rq.kr(0.3, 0.4);
    env = EnvGen.kr(Env.adsr(0.01, 0.2, \amp.kr(0.9), 0.2, 1.1), \gate.kr(1), doneAction: 2);
    sig = Dust2.ar(den!2, env * den.expexp(1e4, 1e6, 0.2, 1.5));
    sig = BPF.ar(sig, \freq.kr(2e3, 0.2)*[1, 0.6], opn, opn.reciprocal);
    sig = Splay.ar(sig, Rand(0.1, 0.4));
    Out.ar(\out.kr(0), sig)
}).add;
SynthDef(\waveBass, {
    | sig env |
    env = EnvGen.kr(Env.asr(\atk.kr(0.1), \amp.kr(0.5), \rel.kr(1)), \gate.kr(1), doneAction: 2);
    sig = Osc.ar(~buf, \freq.kr(100, 0.4)*[1, 2.01], 0, env);
    sig = LeakDC.ar(sig);
    sig = Splay.ar(sig, \spr.kr(0.2, 0.2), 1, \pan.kr(0, 0.2));
    sig = sig * 0.4;
    Out.ar(\out.kr(0), sig)
}).add;

// Sequenciador 
Pdef(\vent,
    Pseq([
        Ppar([
            Pbind(
                \instrument, \vent,
                \dur, Pseq([3/16, 3/16, 3/16, Rest(7/16)+1]),
                \stretch, ~measure,
                \freq, Pexprand(5e3, 2e4),
                \rq, Pwhite(0.3, 0.5),
                \amp, Pseq([1, 0.8, 0.8, \]),
                \group, ~mainGrp,
                \out, ~bus[\rev]
            ),
            Pbind(
                \instrument, \bass,
                \dur, Pseq([3/16, 3/16, 3/16, Rest(7/16)+1]),
                \stretch, ~measure,
                \midinote, 24,
                \rel, 0.1,
                \amp, Pseq((1!3)++[\]),
                \group, ~mainGrp,
                \out, ~bus[\rev]
            )
        ], inf)
    ])
).quant_(~measure*2);
```

## Percussão (chimbal)

Esse é o segundo som a entrar, que simula um chimbal com efeito de _delay_ (ou mais corretamente, de _echo_).

```sclang
SynthDef(\hi-hat, {
    | sig env |
    env = EnvGen.kr(Env.perc(0.01, \rel.kr(0.1), \amp.kr(1)), doneAction: 2);
    sig = WhiteNoise.ar(env!2);
    sig = Balance2.ar(sig[0], sig[1], \pan.kr(0, 0.2), 0.5);
    Out.ar(\out.kr(0), sig)
}).add;

// Synth que vai gerar o efeito de echo
SynthDef(\del, {
    | in sig delay |
    delay = LFDNoise0.kr(2).range(19.midicps.reciprocal, 27.midicps.reciprocal);
    in = In.ar(~bus[\del], 2);
    sig = [in] ++ [CombC.ar(in, delay, delay, 2) * 0.35];
    sig = Splay.ar(sig, 0.2, 1);
    Out.ar(~out, sig);
}).add;

Pdef(\click,
    Pbind(
        \instrument,\click,
        \dur, Pseq([Pseq([1/8, 1/16], 5), 1/16], inf),
        \stretch, ~measure,
        \rel, 0.08,
        \amp, Pseq([Pseq([0.9, Pexprand(0.2, 0.4, 1)], 5), Pexprand(0.2, 0.4, 1)], inf) * 0.4,
        \pan, Prand([-1, 1], inf),
        \group, ~mainGrp,
        \out, ~bus[\del]
    )
).quant_(~measure)
```

## "Coro"

As vozes que aparecem no final, e são programadas em uma estrutura de coral mesmo.

```sclang
SynthDef(\varsaw, {
    | sig env |
    env = EnvGen.kr(Env.asr(0.1, \amp.kr(1), \rel.kr(0.5)), \gate.kr(1), doneAction: 2);
    sig = VarSaw.ar(\freq.kr(440, 0.5)*[1, 1.004], 0, \wid.kr(0.5, 0.6), env);
    sig = Splay.ar(sig, 0.2);
    sig = sig * 0.5;
    Out.ar(\out.kr(0), sig)
}).add;

Pdef(\choir,
    Ppar([
        PmonoArtic(\varsaw, // Baixos
            \dur, Pseq([7/16, Rest(9/16)]++((3/16)!4)++((1/8)!2), inf),
            \stretch, ~measure,
            \midinote, Ptuple([
                Pseq([48, \, 48, 51, 50, 53, 51, 50]), // baixo 1
                Pseq([55, \, 55, 58, 57, 57, 58, 57]), // baixo 2
            ], inf),
            \wid, Pseg([0.5, 1], ~measure*4) ++ Pseq([1], inf),
            \legato, Pseq([0.9, \] ++ (1!5) ++ [0.99], inf),
            \amp, 1,
            \group, ~mainGrp,
            \out, ~bus[\rev]
        ),
        PmonoArtic(\varsaw, // Tenores
            \dur, Pseq([7/16, Rest(9/16), 1/16, 5/16, 3/8, 1/4], inf),
            \stretch, ~measure,
            \midinote, Ptuple([
                Pseq([60, \, 60, 63, 65, 63]), // tenor 1
                Pseq([67, \, 67, 70, 72, 70]), // tenor 2
            ], inf),
            \wid, Pseg([0.5, 1], ~measure*4) ++ Pseq([1], inf),
            \legato, Pseq([0.9, \, 1, 1, 1, 0.9], inf),
            \amp, 1,
            \group, ~mainGrp,
            \out, ~bus[\rev]
        )
    ])
).quant_(~measure*2)
```

## Pulse synth

A melodia percussiva que surge no meio.

```sclang
SynthDef(\pulse, {
    | env sig |
    env = EnvGen.kr(Env.perc(0.02, \rel.kr(0.3), \amp.kr(1)), doneAction: 2);
    sig = Pulse.ar(\freq.kr(440)*[1, 1.008], 0.8, env);
    sig = Splay.ar(sig, \splay.kr(0.4), 0.4);
    Out.ar(\out.kr(0), sig)
}).add;

Pdef(\perc_notes,
    Pbind(
        \instrument, \pulse,
        \dur, Pseq([Pseq([1/8, 1/16, 1/16], 2), Rest(1/8), Pseq([1/16], 6), Rest()], inf),
        \stretch, ~measure,
        \midinote, Pseq([60, 60, 58, 60, 60, 55, \, 62, 63, 65, 63, 62, 63, \], inf),
        \amp, Pseq((1!6)++(0.8!6), inf),
        \rel, Pseq((1.2!7) ++ [1.7, 2, 2.3, 2.3, 2, 1.7, \], inf),
        \group, ~mainGrp,
        \out, ~out
    )
).quant_(~measure*2)
```

## Origem do projeto - trilha alternativa

Antes de se tornar uma música independente, a obra era parte de um projeto coletivo de graduação, feito no 1º semestre de 2020; um exercício de criação de trilha sonora alternativa para um curta ou trecho de filme existente. Nesse caso, o curta em questão pode ser encontrado [aqui](https://www.youtube.com/watch?v=H1mX8ptsmBM), de onde extraímos o vídeo, recriamos toda a sonoplastia, e então a composição da nova trilha.
