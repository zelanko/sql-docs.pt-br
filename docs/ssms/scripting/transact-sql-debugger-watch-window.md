---
title: Janela Inspeção | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Watch Window [Transact-SQL]
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f579b0846c30b72b1bf65d26cf06136932b2dd8f
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328506"
---
# <a name="transact-sql-debugger---watch-window"></a>Depurador do Transact-SQL – janela Inspeção
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  A janela **Inspecionar** exibe informações sobre as expressões que você selecionou. Pode haver até quatro janelas Inspeção: **Inspeção 1**, **Inspeção 2, Inspeção 3** e **Inspeção 4**. As expressões são avaliadas dentro do escopo do quadro de pilha de chamadas atual selecionada na janela **Pilha de Chamadas** . Você deve estar no modo de depuração para inspecionar variáveis e expressões.  
  
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
  
-   As instruções Transact-SQL que retornam um único valor, como: SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
 **Value**  
 Exibe o valor retornado depois que o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] avalia a expressão especificada em **Nome**.  
  
 Se o comprimento de uma expressão for maior do que a largura da coluna **Valor** , uma dica de ferramenta exibe o valor total quando o ponteiro passa sobre a célula **Valor** daquela expressão.  
  
 Um ícone de lupa em uma célula **Valor** indica que o visualizador de depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponível. Na lista, você pode especificar **Visualizador de Texto**, **Visualizador de XML**ou **Visualizador de HTML**. Para iniciar um visualizador de depurador, clique no ícone de lupa. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] abre uma caixa de diálogo que exibe os dados em um formato apropriado para o tipo dos dados.  
  
 **Tipo**  
 Exibe o tipo de dados da expressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Janela Locais](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [Janela Pilha de Chamadas](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Caixa de diálogo QuickWatch](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
