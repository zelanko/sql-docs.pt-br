---
title: Caixa de diálogo QuickWatch
description: Saiba como usar a caixa de diálogo QuickWatch ao depurar o código para exibir rapidamente o tipo de dados e o valor de uma expressão Transact-SQL (como uma variável).
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 79905aa908372f19653f548253d8312b5f760a48
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480617"
---
# <a name="transact-sql-debugger---quickwatch-dialog-box"></a>Depurador do Transact-SQL – caixa de diálogo QuickWatch

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use a caixa de diálogo **QuickWatch** para exibir rapidamente o tipo e o valor de dados de uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] , como uma variável ou parâmetro, quando você estiver depurando um código [!INCLUDE[tsql](../../includes/tsql-md.md)] . Ao observar várias expressões, você também pode acrescentar a expressão à janela **Inspecionar** .  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Lista de Tarefas

 **Para acessar a caixa de diálogo QuickWatch**  
  
-   No menu **Depurar** , clique em **QuickWatch**.  
  
 **Para exibir a informações sobre uma expressão**  
  
1.  Na caixa de listagem **Expressão** , digite ou selecione a expressão desejada. Há suporte às seguintes expressões [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    -   Variáveis.  
  
    -   Parâmetros.  
  
    -   Funções do sistema cujo nome começa com @@.  
  
    -   Expressões criadas pela aplicação de operadores a uma ou mais variáveis, parâmetros ou funções do sistema, como @IntegerCounter + 1 ou FirstName + LastName.  
  
    -   As instruções Transact-SQL que retornam um único valor, como: SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
2.  Clique em **Reavaliar**.  
  
 **Para acrescentar a expressão QuickWatch a uma janela Inspecionar**  
  
-   Clique em **Adicionar Inspeção**.  
  
 **Para alterar o valor da expressão QuickWatch**  
  
-   Clique com o botão direito do mouse na expressão e selecione **Editar Valor**.  
  
## <a name="options"></a>Opções  
 **Lista de expressões**  
 Exibe a expressão atualmente selecionada. A lista suspensa contém um conjunto de expressões que você pode selecionar para exibir. As expressões da lista são as disponíveis no escopo do quadro de pilhas selecionado atualmente na janela **Pilha de Chamadas** . Para exibir uma expressão diferente, digite a expressão ou selecione-a na lista. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte às seguintes expressões: variáveis, parâmetros e funções de sistema com nomes que iniciam com @@.  
  
 **Grade de valor**  
 Exibe as propriedades da expressão atualmente em inspeção.  
  
 **Nome**  
 É a expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] que é inspecionada.  
  
 **Valor**  
 Exibe o valor atribuído atualmente à expressão. Um espaço em branco é exibido se atualmente a expressão não tiver nenhum valor.  
  
 Se o comprimento de uma expressão for maior do que a largura da coluna **Valor** , uma dica de ferramenta exibe o valor total quando o ponteiro passa sobre a célula **Valor** daquela expressão.  
  
 Um ícone de lupa em uma célula **Valor** indica que o visualizador de depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponível. Na lista, você pode especificar **Visualizador de Texto**, **Visualizador de XML** ou **Visualizador de HTML**. Para iniciar um visualizador de depurador, clique no ícone de lupa. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] abre uma caixa de diálogo que exibe os dados em um formato apropriado para o tipo dos dados.  
  
 **Tipo**  
 Exibe o tipo de dados da expressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](./transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](./transact-sql-debugger-information.md)   
 [Janela de Observação](./transact-sql-debugger-watch-window.md)   
 [Janela Locais](./transact-sql-debugger-locals-window.md)   
 [Janela Pilha de Chamadas](./transact-sql-debugger-call-stack-window.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
