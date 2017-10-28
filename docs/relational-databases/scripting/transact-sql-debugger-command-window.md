---
title: Janela Comando | Microsoft Docs
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
- VS.CommandWindow
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 328c018f1b1b62ce578f849e88301d554142ee00
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="transact-sql-debugger---command-window"></a>Depurador do Transact-SQL – Janela Comando
  Use a **Janela Comando** para executar comandos como de depuração e edição na janela do Editor de Consultas do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está atualmente em depuração. É necessário estar no modo de depuração para usar a **Janela Comando**. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte a muitos dos comandos que também têm suporte na janela [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Command** window. Para obter mais informações, veja [Janela Comando do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=112007).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a Janela de Comando**  
  
-   No menu **Depurar** , clique em **Iniciar Depuração**.  
  
 **Para imprimir o valor de uma variável**  
  
-   No **CommandWindow**, digite **Debug.Print \<VariableName>** e pressione ENTER.  
  
 **Para listar as informações sobre a thread atual**  
  
-   Na **Janela Comando**, digite **Debug.ListThread**e pressione ENTER.  
  
 **Para adicionar uma variável à janela QuickWatch.**  
  
-   Na **CommandWindow**, digite **Debug.QuickWatch \<VariableName>** e pressione ENTER.  
  
## <a name="see-also"></a>Consulte também  
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  

