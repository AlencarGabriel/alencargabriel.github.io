---
title: "Apresentação MsgTimer para Advpl - Protheus"
published: true
tags: [msgtimer, advpl, totvs, protheus]
author: "Gabriel Alencar"
header-img: "img/Usando_Outline_AdvPl_VsCode.png"
---

**Olá mundo**, neste artigo vou apresentar um novo projeto que criei para suprir uma necessidade de um cliente, porém a implementação serve para muitos outros casos. Acredito que você já deve ter passado por pelo menos um dos exemplos (casos) que apresentarei abaixo.

Espero que goste e ajude!

---

Existem muitas coisas na área de desenvolvimento - feito pelos programadores - que me deixa bem chateado, uma delas são <u>mensagens que dependem de uma interação com o usuário no meio de um Loop de processamento ou dentro de uma transação</u>.

Se você já fez isso, parabéns! Com certeza você já deve ter atrasado a vida de alguém, ou sofrido para descobrir o porque de tanto *lock* em seu sistema sempre que uma rotina X era executada.

Imaginem o seguinte questionamento de um usuário que pode ser real: "Estou importando um arquivo, e para cada linha aparece a seguinte mensagem: Cliente C bloqueado! Deseja continuar (Sim/Não), dependendo da quantidade de registros não da tempo nem de ir no banheiro". :confused:

Não seria mais fácil se antes do processamento ou início da transação, aparecesse uma mensagem apenas para o usuário perguntando se era para ignorar os clientes bloqueados ou não? :grin:

Agora imaginem o seguinte caso: No meio de um processamento aparece uma mensagem de erro (violação de uma regra de negócio por exemplo), até ai tudo bem! Só que o processamento demora um certo tempo para finalizar, e o usuário não viu a mensagem. Porém, essa mensagem estava dentro de uma transação, antes que um *Disarm Transaction* ou *Rollback* da transação fosse feito. Dependendo da demora do usuário de simplesmente "Fechar" a mensagem ou o uso das tabelas envolvidas, irá ocorrer uma série de travamentos no sistema que poderá inclusive afetar outros usuários em outros processamentos.

Bem, nesse caso é simples! Basta então desarmar a transação antes de exibir a mensagem! Ai o usuário pode demorar o tempo que for para interagir com a mensagem que não impactará com os demais colegas! :clap:

#### Resumo: Mensagem que depende de interação com usuário no meio de processamento, ou dentro de transação não é uma boa prática de desenvolvimento!

**"Ah Gabriel, mas existem casos onde eu realmente preciso colocar uma mensagem no meio do Loop."**

Realmente, concordo com você que existem casos exporádicos, onde realmente a única alternativa para o Processo, Regra de Negócio ou ainda limitação de recursos na linguagem seja sim necessário ter uma mensagem, e é sobre isso que esse artigo tem a função de falar.

Muitas vezes colocamos mensagens informativas em nossos programas onde se o usuário viu ou não aquela mensagem, o resultado se torna indiferente. As vezes ele clicou em processar, saiu da mesa para fazer outra coisa pois o processo é demorado, mas a rotina mostrou uma mensagem de questionamento. Quando ele volta para verificar se finalizou, na verdade nem havia começado. Sendo assim, existem certas mensagens que aparecendo ou não, não impactam no processo, e poderiam ter sido fechadas automaticamente, evitando um atraso no trabalho do cliente.

Então, para auxiliar de forma simples e de menor impacto nos exemplos citados anteriormente criei a função [MsgTimer](https://github.com/AlencarGabriel/advpl-MsgTimer). Onde esta funciona de forma semelhante as funções MVC de mensagem do Protheus 12: FwAlertError, FwAlertInfo, FwAlertSucces e FwAlertWarning, com o diferencial do temporizador para fechar a mensagem e a possibilidade de relacionar qualquer ícone com os botões suportados (nas funções padrões os ícones são específicos de cada função).

Segue a documentação da rotina contendo todos os detalhes e informações de uso e parâmetros: https://github.com/AlencarGabriel/advpl-MsgTimer#documentação

### Comparação entre MsgTimer (com tipo Error) e FwAlertError:

![MsgTimer Error](https://github.com/AlencarGabriel/advpl-MsgTimer/raw/master/Examples/MsgTimer_Error_Default.png) ![FwAlertError](https://github.com/AlencarGabriel/advpl-MsgTimer/raw/master/Examples/FwAlertError.png)


Espero ter ajudado, em breve mais artigos explicando outros macetes que utilizo. Até a próxima! :computer: :wave:
