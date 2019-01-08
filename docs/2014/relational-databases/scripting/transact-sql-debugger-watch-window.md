---
title: Janela Inspeção | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Watch Window [Transact-SQL]
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01caaf26257c06aae8cb7668693fd3ff6b8b5135
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328746"
---
# <a name="watch-window"></a>Janela de Observação
  A janela **Inspecionar** exibe informações sobre as expressões que você selecionou. Pode haver até quatro janelas de inspeção: **Assista a 1**, **Assista a 2, 3 de assistir**, e **Assista 4**. As expressões são avaliadas dentro do escopo do quadro de pilha de chamadas atual selecionada na janela **Pilha de Chamadas** . Você deve estar no modo de depuração para inspecionar variáveis e expressões.  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar as janelas Inspecionar**  
  
-   No menu **Depurar** , clique em **Janelas**, clique em **Inspecionar**e depois em **Inspecionar 1**, **Inspecionar 2, Inspecionar 3**ou **Inspecionar 4**.  
  
 **Para alterar o valor de uma expressão**  
  
-   Clique com o botão direito do mouse na expressão e selecione **Editar Valor**.  
  
## <a name="columns"></a>Colunas  
 **Nome**  
 São as expressões listadas pelo depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] . Há suporte para as seguintes expressões:  
  
-   Variáveis.  
  
-   Parâmetros.  
  
-   Funções do sistema cujo nome começa com @@.  
  
-   Expressões criadas pela aplicação de operadores a uma ou mais variáveis, parâmetros ou funções do sistema, como @IntegerCounter + 1 ou FirstName + LastName.  
  
-   Instruções Transact-SQL que retornam um único valor, como: SELECT CharacterCol FROM MyTable onde PrimaryKey = 1.  
  
 **Value**  
 Exibe o valor retornado depois que o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] avalia a expressão especificada em **Nome**.  
  
 Se o comprimento de uma expressão for maior do que a largura da coluna **Valor** , uma dica de ferramenta exibe o valor total quando o ponteiro passa sobre a célula **Valor** daquela expressão.  
  
 Um ícone de lupa em uma célula **Valor** indica que o visualizador de depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponível. Na lista, você pode especificar **Visualizador de Texto**, **Visualizador de XML**ou **Visualizador de HTML**. Para iniciar um visualizador de depurador, clique no ícone de lupa. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] abre uma caixa de diálogo que exibe os dados em um formato apropriado para o tipo dos dados.  
  
 **Tipo**  
 Exibe o tipo de dados da expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)   
 [Janela Locais](transact-sql-debugger-locals-window.md)   
 [Janela Pilha de Chamadas](transact-sql-debugger-call-stack-window.md)   
 [Caixa de diálogo QuickWatch](transact-sql-debugger-quickwatch-dialog-box.md)   
 [Expressões &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
