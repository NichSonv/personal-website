---
title: "Golang simple form"
desc: "Simples captador de lead"
date: 2023-01-19T14:56:15-03:00
draft: false
keywords: ""
weight: 0
hidden: false
---
# {{< param title >}}

```golang
func main() {
	pl("Hello! Do you wish to fill this form? Y/N")
	sc(&consign); p("\n")
	if !(consign == "Y" || consign == "y" || consign == "N" || consign == "n") {
		pl(err)
		main()
	}
	switch consign {
	case "Y","y":
		dataGet()
	case "N","n":
		pl("Alright, have a nice day!")
		os.Exit(0)
	}
}
```

Esse é um programa muito simples que escrevi em Golang, como um exercício prático de aprendizado da linguagem. Trata-se de um programa básico de captação de lead, que interage com o usuário em busca das informações necessárias.  
No link abaixo você pode baixar o programa e testá-lo em sua própria máquina:

<a href="lead" download>Lead (unix program) - download</a>

Para ver o código completo dentro do GitHub, clique [aqui](https://github.com/NichSonv/go-snippets/blob/main/leadForm/lead.go).
