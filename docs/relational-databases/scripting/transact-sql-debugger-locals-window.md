---
title: Janela Locais | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.locals
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 84668538d8c13c4317eec610afabcdf39d457899
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-debugger---locals-window"></a>Depurador do Transact-SQL – janela Locais
  A janela **Locais** exibe informações sobre as expressões locais no escopo atual do depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] . O escopo é definido como o quadro atual da pilha de chamadas selecionada na janela **Pilha de Chamadas** . Você deve estar no modo de depuração para exibir as expressões locais.  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a janela Locais**  
  
-   No menu **Depurar** , clique em **Janelas**e em **Locais**.  
  
 **Para alterar o valor de uma expressão**  
  
-   Clique com o botão direito do mouse na expressão e selecione **Editar Valor**.  
  
## <a name="columns"></a>Colunas  
 **Nome**  
 É o nome da expressão local. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] lista variáveis, parâmetros e funções de sistema com nomes que iniciam com @@.  
  
 **Value**  
 Exibe o valor atribuído atualmente à expressão local. Esta coluna fica em branco quando nenhum valor é atribuído à expressão.  
  
 Se o comprimento de uma expressão for maior do que a largura da coluna **Valor** , uma dica de ferramenta exibe o valor total quando o ponteiro passa sobre a célula **Valor** daquela expressão.  
  
 Um ícone de lupa em uma célula **Valor** indica que o visualizador de depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponível. Na lista, você pode especificar **Visualizador de Texto**, **Visualizador de XML**ou **Visualizador de HTML**. Para iniciar um visualizador de depurador, clique no ícone de lupa. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] abre uma caixa de diálogo que exibe os dados em um formato apropriado para o tipo dos dados.  
  
 **Tipo**  
 Exibe o tipo de dados da expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Janela de Observação](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [Janela Pilha de Chamadas](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Caixa de diálogo QuickWatch](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
