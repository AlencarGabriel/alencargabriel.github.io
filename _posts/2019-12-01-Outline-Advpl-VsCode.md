---
title: "Usando Outline com AdvPl no VsCode"
published: true
tags: [vscode, advpl, totvs]
author: "Gabriel Alencar"
header-img: "img/Usando_Outline_AdvPl_VsCode.png"
---

**Olá mundo**, neste artigo vou falar sobre um método que estou utilizando para implementar o recurso "Outline" ou a listagem de variáveis e métodos, funções, etc do VsCode enquanto o Language Server para AdvPL não fica pronto.

Espero que goste!

---

Para aqueles que não sabem sobre o que este artigo se trata, vou explicar.
A visão Outline ou a listagem de símbolos do VsCode é um recurso nativo do VsCode que permite encontrar os símbolos da linguagem (métodos, classes, variáveis, etc) de forma mais "rápida" e ágil. 

![image](https://user-images.githubusercontent.com/10109480/69922116-f60e0880-1477-11ea-9b58-60334b07899f.png)

Porém, seu funcionamento só é possível quando há implementado via Language Server os recursos para que o VsCode entenda a sintaxe e estrutura do AdvPL como qualquer outra linguagem já suportada por ele (Java Script, Type Script, ...)

Sendo assim, enquanto esse recurso não fica disponível para as extensões de suporte a AdvPL [advpl-vscode](https://github.com/totvs/advpl-vscode) ou [tds-vscode](https://github.com/totvs/tds-vscode), existe uma forma de utilizar este "recurso" de uma outra forma, e é sobre isso que vamos falar agora.

- Como pré-requisito, você precisará instalar a extensão [CodeMap](https://marketplace.visualstudio.com/items?itemName=oleg-shilo.codemap).

- Instalado a extensão, baixe o arquivo de mapeamento dos símbolos AdvPL [mapper_prw.js](https://gist.github.com/AlencarGabriel/d6f7c8c192886cb343f377c7ee9bfc74) e adicione na pasta do VsCode **AppData\Roaming\Code\User** , ou em seu diretório de preferência.

- Baixado o arquivo, basta configurar a extensão para que ela carregue a configuração dos símbolos AdvPL da seguinte forma: 

```json
  "codemap.prw": "C:\\Users\\MyUSer\\AppData\\Roaming\\Code\\User\\mapper_prw.js",
  "codemap.prx": "C:\\Users\\MyUser\\AppData\\Roaming\\Code\\User\\mapper_prw.js",
  "codemap.textMode": false
```

- Pronto, agora basta carregar um fonte AdvPL e na Activity Bar estará sendo apresentado a estrutura do código conforme hierarquia.

![image](https://user-images.githubusercontent.com/10109480/69922409-c9a7bb80-147a-11ea-8b5c-7c8e0f5e7f7f.png)

> Clicando em cada item, o cursor do documento será posicionado para a linha ao qual ele pertence. 

> Fiz uma implementação recente para que os métodos das classes fiquem dispostos abaixo da assinatura da classe, isso porque em AdvPL os métodos da classe são definidos utilizando a palavra `Class`, e a declaração do mesmo pode estar em qualquer lugar do código.

Espero ter ajudado, em breve mais artigos explicando outros macetes que utilizo. Até a próxima! :computer: :wave:
