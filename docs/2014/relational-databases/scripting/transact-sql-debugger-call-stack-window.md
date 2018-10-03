---
title: Janela Pilha de Chamadas| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.callstack
helpviewer_keywords:
- Call Stack Window [Transact-SQL]
ms.assetid: ddb0b19c-87cd-4883-bcb8-ec09ffb30369
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2f69398562a11c466d3772389c326b32cb6e6cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220716"
---
# <a name="call-stack-window"></a>Janela Pilha de Chamadas
  A janela **Pilha de Chamadas** exibe os módulos da pilha de chamadas e os valores e tipos de dados de quaisquer parâmetros que passaram para os módulos. [!INCLUDE[tsql](../../includes/tsql-md.md)] os módulos incluem procedimentos armazenados, funções e gatilhos. Para exibir a pilha de chamadas, você deve estar no modo de depuração.  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a janela Pilha de Chamadas**  
  
-   No menu **Depurar** , clique em **Janelas**e em **Pilha de Chamadas**.  
  
 **Para alterar o quadro atual da Pilha de Chamadas**  
  
 Você pode usar qualquer um dos seguintes procedimentos para montar o quadro atual do quadro de pilhas:  
  
-   Clique com o botão direito do mouse no registro de ativação e depois clique em **Alternar para Quadro**.  
  
-   Clique duas vezes no quadro de pilhas.  
  
 **Para exibir a origem de um quadro diferente do quadro atual**  
  
-   Clique com o botão direito do mouse no registro de ativação e depois clique em **Ir para Código-Fonte**.  
  
## <a name="stack-frames"></a>Quadros de pilhas  
 Cada linha na janela **Pilha de Chamadas** é chamada de um registro de ativação e representa a chamada de um módulo de um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] ou uma chamada de um módulo a outro. O registro de ativação inferior no vídeo indica a linha da janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que fez a primeira chamada na pilha. A linha superior indica em qual linha o depurador pausou a depuração e é identificada por uma seta amarela na margem esquerda da janela. Cada linha intermediária indica o módulo e o número de linha do código fonte que chamou o próximo quadro de pilha mais alto.  
  
 Todas as expressões nas janelas **Locais**, **Inspecionar**e **QuickWatch** são avaliadas com base no registro de ativação atual. A janela Editor de Consultas exibe o código para o quadro atual. Por padrão, o registro de ativação atual é o quadro no qual o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] pausou a execução. Quando você altera o registro de ativação atual para outro quadro, as expressão das janelas **Locais**, **Inspecionar**e **QuickWatch** são reavaliadas no contexto do novo quadro de pilhas e o código-fonte do novo quadro é exibido na janela Editor de Consultas.  
  
## <a name="columns"></a>Colunas  
 **Nome**  
 Exibe informações sobre um módulo na pilha de chamadas.  
  
 Na linha inferior da pilha de chamadas, **Nome** relaciona a janela de fonte do Editor de Consultas e o número de linha que fez a primeira chamada na pilha. Para as outras linhas, **Nome** apresenta o formato **Module(Instance.Database)(ParmList) LineNumber**.  
  
 **Módulo**  
 É o nome do procedimento armazenado, função ou procedimento armazenado que chamou o próximo quadro.  
  
 **Instance.Database**  
 É a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e do banco de dados que está segurando o módulo.  
  
 **ParmList**  
 Indica o tipo de dados, o nome e o valor de cada parâmetro transmitido dentro durante a chamada para o módulo.  
  
 **LineNumber**  
 Para todas as linhas excluindo a linha de parte superior, **LineNumber** indica qual linha no módulo chamou o quadro. Para a linha de parte superior, **LineNumber** indica a linha na qual o depurador está atualmente focalizado.  
  
 **Idioma**  
 Exibe **Transact-SQL** para [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)   
 [Percorrer código Transact-SQL](step-through-transact-sql-code.md)  
  
  
