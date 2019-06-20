---
title: Janela Comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a66709cc090f39a41e5bee5b52a779b8d2f6764
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063534"
---
# <a name="command-window"></a>Janela Comando
  Use a **Janela Comando** para executar comandos como de depuração e edição na janela do Editor de Consultas do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está atualmente em depuração. É necessário estar no modo de depuração para usar a **Janela Comando**. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte a muitos dos comandos que também têm suporte na janela [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Command** window. Para obter mais informações, veja [Janela Comando do Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a Janela de Comando**  
  
-   No menu **Depurar** , clique em **Iniciar Depuração**.  
  
 **Para imprimir o valor de uma variável**  
  
-   No **CommandWindow**, digite **Debug.Print \<VariableName>** e pressione ENTER.  
  
 **Para listar as informações sobre a thread atual**  
  
-   No **CommandWindow**, digite `Debug.ListThread`, e pressione ENTER.  
  
 **Para adicionar uma variável à janela QuickWatch.**  
  
-   Na **CommandWindow**, digite **Debug.QuickWatch \<VariableName>** e pressione ENTER.  
  
## <a name="see-also"></a>Consulte também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)  
