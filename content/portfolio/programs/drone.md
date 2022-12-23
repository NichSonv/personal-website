---
title: "Drone.scd"
listag: "-C-I"
date: 2022-12-17T22:49:17-03:00
draft: false
keywords: "-, nicholas, sonvezzo, somvezzo, som-vezzo, -"
weight: 0
hidden: false
---
# Drone.scd - Instrumento virtual

{{< gist NichSonv "1d0501e682b0f6be6268408d43cf48da" "drone.scd" >}}

O instrumento virtual \drone se trata de um sintetizador que programei em SuperCollider (_sclang_), e que se aproveita do efeito acústico da seleção de harmônicos em um som complexo.  
O principal objeto em sua construção, e que é a base da sua sonoridade, é o _Formant_, e nada mais é que um oscilador de som complexo com um filtro embutido, cuja abertura de banda e frequência ressonante podem ser alterados. O instrumento utiliza esse oscilador em conjunto com um reverb e controle de espacialização, e aí está criada a sua sonoridade característica.

Abaixo um exemplo do instrumento em prática, em uma versão da obra [Atmosphere]({{< ref "atmosphere.md" >}}) (ouça com fones de ouvido para uma melhor experiência):

{{< soundcloud src="1036050955" href="atmosphere" title="Atmosphere" >}}