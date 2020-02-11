---
title: Janela Locais
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44aedf7d53b2a9ad91b37f5023c13d8e20097da1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75243046"
---
# <a name="locals-window"></a>Janela Locais
  A janela **Locais** exibe informações sobre as expressões locais no escopo atual do depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] . O escopo é definido como o quadro atual da pilha de chamadas selecionada na janela **Pilha de Chamadas** . Você deve estar no modo de depuração para exibir as expressões locais.  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a janela Locais**  
  
-   No menu **Depurar** , clique em **Janelas**e em **Locais**.  
  
 **Para alterar o valor de uma expressão**  
  
-   Clique com o botão direito do mouse na expressão e selecione **Editar Valor**.  
  
## <a name="columns"></a>Colunas  
 **Nome**  
 É o nome da expressão local. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] lista variáveis, parâmetros e funções de sistema com nomes que iniciam com @@.  
  
 **Valor**  
 Exibe o valor atribuído atualmente à expressão local. Esta coluna fica em branco quando nenhum valor é atribuído à expressão.  
  
 Se o comprimento de uma expressão for maior do que a largura da coluna **Valor** , uma dica de ferramenta exibe o valor total quando o ponteiro passa sobre a célula **Valor** daquela expressão.  
  
 Um ícone de lupa em uma célula **Valor** indica que o visualizador de depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponível. Na lista, você pode especificar **Visualizador de Texto**, **Visualizador de XML**ou **Visualizador de HTML**. Para iniciar um visualizador de depurador, clique no ícone de lupa. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] abre uma caixa de diálogo que exibe os dados em um formato apropriado para o tipo dos dados.  
  
 **Tipo**  
 Exibe o tipo de dados da expressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)   
 [Janela de Observação](transact-sql-debugger-watch-window.md)   
 [Janela Pilha de Chamadas](transact-sql-debugger-call-stack-window.md)   
 [Caixa de diálogo QuickWatch](transact-sql-debugger-quickwatch-dialog-box.md)   
 [Expressões &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
