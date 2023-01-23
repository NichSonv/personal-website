---
title: "OscMusicPlayer.scd - WIP"
desc: "Interface para performance de música 'osciloscópica'"
date: 2022-12-24T18:58:55-03:00
draft: false
keywords: ""
weight: 0
hidden: false
---
# OscMusic player

**Esse é um trabalho em andamento.**

O _OscMusic player_ se trata de uma interface e instrumento virtual, para se criar "música de osciloscópio" (em inglês, _oscilloscope music_).

```sclang
SynthDef(\xyzSin, {
	var sig, env, hz;
	env = Env.asr(0.1, 1, 0.2).kr(2, \gate.kr(1));
	sig = SinOsc.ar(\freq.kr(~hzs[0]), [\ph0.kr(~ph0[0]), \ph1.kr(~ph1[0])], env);
	sig = Pan2.ar(sig, [\pan0.kr(~pan0[0]), \pan1.kr(~pan1[0])], \amp.kr(~amps[0]));
	Out.ar(\out.kr(0), sig)
}).add;
```

[Código completo](https://github.com/NichSonv/osc-music-interface).