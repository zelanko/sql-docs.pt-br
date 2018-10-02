---
title: Janela Locais | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.locals
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2285b8a55a1162a49b96c41e1fb81b5e5fc5931f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710304"
---
# <a name="transact-sql-debugger---locals-window"></a>Depurador do Transact-SQL – janela Locais
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Janela de Observação](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [Janela Pilha de Chamadas](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Caixa de diálogo QuickWatch](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
