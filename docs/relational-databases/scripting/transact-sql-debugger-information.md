---
title: "Informações do depurador Transact-SQL | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Transact-SQL debugger, Locals Window
- Transact-SQL debugger, Watch Window
- Transact-SQL debugger, Threads Window
- Transact-SQL debugger, Call Stack Window
- Transact-SQL debugger, QuickWatch
- Transact-SQL debugger, viewing information
ms.assetid: b99819cc-f388-41a1-b304-36e78ce24147
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 706952bff0744cb88d12a624ba4c68363cb85652
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-debugger---information"></a>Depurador do Transact-SQL – Informações
  Toda vez que o depurador pausa a execução em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] específica, você pode usar as várias janelas do depurador para exibir o estado de execução atual.  
  
## <a name="debugger-windows"></a>Janelas do depurador  
 Em modo de depurador, o depurador abre duas janelas na parte inferior da janela principal do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . O depurador exibe toda as suas informações nessas duas janelas. Cada uma das janelas de depurador tem guias que você pode selecionar para controlar o conjunto de informações exibido na janela. A janela esquerda do depurador contém as guias **Locais**, **Inspecionar 1**, **Inspecionar 2**, **Inspecionar 3**e **Inspecionar 4** . A janela direita do depurador contém as guias **Pilha de Chamadas**, **Threads**, **Pontos de Interrupção**, **Janela de Comando**e **Saída** .  
  
> [!NOTE]  
>  As descrições anteriores aplicam-se aos locais padrões das janelas do depurador. Você pode arrastar uma guia para movê-la de uma janela para outra ou desencaixar uma guia para criar uma nova janela, que você pode colocar onde desejar.  
  
 Por padrão, nem todas essas guias ou janelas são ativas. Você pode abrir uma janela específica usando qualquer uma das seguintes maneiras:  
  
-   No menu **Depurar** , clique em **Windows**e selecione a janela desejada.  
  
-   Na barra de ferramentas de **Depurar** , clique em **Pontos de Interrupção**e selecione a janela desejada.  
  
## <a name="transact-sql-expressions"></a>Expressões Transact-SQL  
 Expressões são cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] que são avaliadas como um valor escalar simples, como, por exemplo, variáveis ou parâmetros. A janela esquerda do depurador pode exibir os valores dos dados que são atribuídos no momento a expressões em até cinco guias ou janelas: **Locais, Inspecionar 1**, **Inspecionar 2**, **Inspecionar 3**e **Inspecionar 4**.  
  
 A janela **Locais** exibe informações sobre os variáveis locais no escopo atual do depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] . O conjunto de expressões listadas na janela **Locais** é alterado à medida que o depurador é executado por meio de partes diferentes do código.  
  
 As expressões no **QuickWatch** e nas quatro janelas **Inspecionar** não se limitam apenas a listar o identificador de uma variável. Você pode especificar uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] que é avaliada para um único valor, como somar um número para uma variável, ou uma instrução SELECT que é avaliada para um único valor. Os exemplos incluem:  
  
-   O nome de uma variável, como @IntegerCounter.  
  
-   Uma operação aritmética em uma variável, como @IntegerCounter + 1.  
  
-   Uma operação de cadeia de caracteres em duas variáveis de caractere, como @FirstName + @LastName.  
  
-   Uma instrução SELECT que retorna um único valor, como SELECT CharCol FROM MyTable WHERE PrimaryKey = 1.  
  
 Você pode usar a janela **QuickWatch** para exibir o valor de uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] e salvar essa expressão em uma janela **Inspeção** . Para selecionar uma expressão em **QuickWatch**, selecione ou digite o nome da expressão na caixa **Expressão** .  
  
 As quatro janelas **Inspecionar** exibem informações sobre variáveis e expressões que você selecionou. O conjunto de expressões listadas nas janelas **Inspecionar** só será alterado se você adicionar ou excluir expressões da lista.  
  
 Para adicionar uma expressão a uma janela **Inspeção** , você pode selecionar **Adicionar Inspeção** , na caixa de diálogo **QuickWatch** , ou inserir o nome da expressão na coluna **Nome** de uma linha vazia em uma janela **Inspeção** .  
  
 Você pode definir valores de dados para variáveis nas janelas **Locais**, **Inspecionar**ou **QuickWatch** , clicando com o botão direito na linha e selecionando **Editar Valor**. As colunas **Valor** , na janela **Locais** , janela **Inspeção** e a caixa de diálogo **QuickWatch** dão suporte a visualizadores de dados em texto, XML e HTML. Os visualizadores são representados por um dica de dados à direita da coluna **Valores** . Você pode usar os visualizadores para exibir valores de dados em texto, XML ou HTML em exibições que correspondam aos tipos de dados, por exemplo, exibindo arquivos XML em uma janela do navegador.  
  
 No modo de depuração, quando você move o ponteiro do mouse sobre um identificador, uma pop-up **Informações Rápidas** é exibida com o nome da expressão e seu valor atual. Para obter mais informações, veja [Informações rápidas &#40;IntelliSense&#41;](../../relational-databases/scripting/quick-info-intellisense.md).  
  
## <a name="breakpoints"></a>Pontos de interrupção  
 Você pode usar a janela **Pontos de Interrupção** para exibir e gerenciar os pontos de interrupção definidos no momento. Para obter mais informações, veja [Percorrer código Transact-SQL](../../relational-databases/scripting/step-through-transact-sql-code.md).  
  
## <a name="call-stacks"></a>Pilhas de Chamadas  
 A janela **Pilha de Chamadas** exibe o local de execução atual e informações sobre como a execução foi transmitida da janela do editor original por meio de qualquer módulo do [!INCLUDE[tsql](../../includes/tsql-md.md)] (funções, procedimentos armazenados ou gatilhos) para alcançar o local de execução atual. Cada linha na janela **Pilha de Chamadas** é chamada de um registro de ativação e representa qualquer um dos seguintes itens:  
  
-   O local de execução atual.  
  
-   Uma chamada de um módulo para outro.  
  
-   Uma chamada em uma janela do editor para um módulo [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 A ordem da pilha é inversa àquela em que os módulos foram chamados. O local de execução atual é na parte superior da pilha, e a chamada original, na parte inferior. Uma seta amarela na margem esquerda do quadro de pilha identifica o quadro no qual o depurador pausou a execução.  
  
 A coluna **Nome** registra as seguintes informações:  
  
-   O módulo de origem que contém a linha de código que chamou para o próximo nível.  
  
-   A linha de código que chamou o próximo módulo na pilha.  
  
-   Se a chamada veio de um procedimento armazenado ou de uma função que utilizou os parâmetros, os nomes, os tipos de dados e os valores de todos os parâmetros também são listadas.  
  
 As expressões nas janelas **Locais**, **Inspecionar**e **QuickWatch** são avaliadas quanto ao registro de ativação atual. Por padrão, o quadro de pilhas atual é o quadro superior da pilha, em que o depurador pausou a execução. Quando você especifica outro registro de ativação como o quadro atual, as expressão das janelas **Locais**, **Inspecionar**e **QuickWatch** são reavaliadas para o novo registro de ativação. Você pode alterar o registro de ativação atual clicando duas vezes em um quadro ou clicando em um quadro e selecionando **Alternar para Quadro**. Nesse ponto, as expressões das janelas **Locais**, **Inspecionar**e **QuickWatch** são reavaliadas para o novo quadro. Sempre que um quadro de pilhas atual não está no quadro superior na pilha, uma seta verde na margem esquerda do quadro de pilhas identifica o quadro de pilhas atual.  
  
 Quando você clica com o botão direito do mouse no registro de ativação e seleciona **Ir para Código-fonte**, o código desse quadro é exibido em uma janela do Editor de Consultas. No entanto, esse quadro não se transforma no quadro atual, e o conteúdo das janelas **Locais**, **Inspecionar**e **QuickWatch** não é alterado.  
  
## <a name="system-information-and-transact-sql-results"></a>Informações do sistema e resultados de Transact-SQL  
 O depurador lista seu status e mensagens de evento na janela **Saída** . Isso inclui informações, como, por exemplo, quando o depurador é anexado a outros processos ou quando o thread do depurador termina.  
  
 Em modo de depuração, as guias **Resultados** e **Mensagens** ainda ficam ativas no Editor de Consultas. A guia **Resultados** continua a exibir os conjuntos de resultados das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que são executados durante uma sessão de depuração. A guia **Mensagens** continua a exibir mensagens de sistema, como, por exemplo, *xx* Linhas Afetadas e a saída de instruções PRINT e RAISERROR.  
  
## <a name="see-also"></a>Consulte também  
 [Janela Locais](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [Janela de Observação](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [Caixa de diálogo QuickWatch](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [Janela Pontos de Interrupção](../../relational-databases/scripting/transact-sql-debugger-breakpoints-window.md)   
 [Janela Pilha de Chamadas](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Janela Threads](../../relational-databases/scripting/transact-sql-debugger-threads-window.md)   
 [Janela Saída](../../relational-databases/scripting/transact-sql-debugger-output-window.md)   
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
