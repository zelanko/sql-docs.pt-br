---
title: Caixa de diálogo QuickWatch
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d41aab8066b4ce1ee4e45fa9c363e60479868a5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243040"
---
# <a name="quickwatch-dialog-box"></a>Caixa de diálogo QuickWatch
  Use a caixa de diálogo **QuickWatch** para exibir rapidamente o tipo de dados e o [!INCLUDE[tsql](../../includes/tsql-md.md)] valor de uma expressão, como uma variável ou parâmetro, quando você [!INCLUDE[tsql](../../includes/tsql-md.md)] estiver depurando o código. Ao observar várias expressões, você também pode acrescentar a expressão à janela **Inspecionar** .  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a caixa de diálogo QuickWatch**  
  
-   No menu **Depurar** , clique em **QuickWatch**.  
  
 **Para exibir as informações sobre uma expressão**  
  
1.  Na caixa de listagem **Expressão** , digite ou selecione a expressão desejada. Há suporte às seguintes expressões [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    -   Variáveis.  
  
    -   Parâmetros.  
  
    -   Funções do sistema cujo nome começa com @@.  
  
    -   Expressões criadas pela aplicação de operadores a uma ou mais variáveis, parâmetros ou funções do sistema, como @IntegerCounter + 1 ou FirstName + LastName.  
  
    -   Instruções Transact-SQL que retornam um único valor, como: SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
2.  Clique em **Reavaliar**.  
  
 **Para adicionar a expressão QuickWatch a um janela Inspeção**  
  
-   Clique em **Adicionar Inspeção**.  
  
 **Para alterar o valor da expressão QuickWatch**  
  
-   Clique com o botão direito do mouse na expressão e selecione **Editar Valor**.  
  
## <a name="options"></a>Opções  
 **Lista de expressões**  
 Exibe a expressão atualmente selecionada. A lista suspensa contém um conjunto de expressões que você pode selecionar para exibir. As expressões da lista são as disponíveis no escopo do quadro de pilhas selecionado atualmente na janela **Pilha de Chamadas** . Para exibir uma expressão diferente, digite a expressão ou selecione-a na lista. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte às seguintes expressões: variáveis, parâmetros e funções de sistema com nomes que iniciam com @@.  
  
 **Grade de valores**  
 Exibe as propriedades da expressão atualmente em inspeção.  
  
 **Nomes**  
 É a expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] que é inspecionada.  
  
 **Valor**  
 Exibe o valor atribuído atualmente à expressão. Um espaço em branco é exibido se atualmente a expressão não tiver nenhum valor.  
  
 Se o comprimento de uma expressão for maior do que a largura da coluna **Valor** , uma dica de ferramenta exibe o valor total quando o ponteiro passa sobre a célula **Valor** daquela expressão.  
  
 Um ícone de lupa em uma célula **Valor** indica que o visualizador de depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponível. Na lista, você pode especificar **Visualizador de Texto**, **Visualizador de XML**ou **Visualizador de HTML**. Para iniciar um visualizador de depurador, clique no ícone de lupa. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] abre uma caixa de diálogo que exibe os dados em um formato apropriado para o tipo dos dados.  
  
 **Escreva**  
 Exibe o tipo de dados da expressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)   
 [Janela de inspeção](transact-sql-debugger-watch-window.md)   
 [Janela locais](transact-sql-debugger-locals-window.md)   
 [Janela pilha de chamadas](transact-sql-debugger-call-stack-window.md)   
 [Expressões &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/expressions-transact-sql)  
  
  
