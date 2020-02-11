---
title: Janela Comando
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 26306f8ad2adf01ebdcbf1b52169f1c2ec964920
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75243076"
---
# <a name="command-window"></a>Janela Comando
  Use o **janela comando** para executar comandos, como comandos debug e Edit, em relação ao código na janela [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] do editor de consultas que está sendo depurada no momento. É necessário estar no modo de depuração para usar a **Janela Comando**. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte a muitos dos comandos que também têm suporte na janela [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Command** window. Para obter mais informações, veja [Janela Comando do Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para acessar a janela de comando**  
  
-   No menu **Depurar** , clique em **Iniciar Depuração**.  
  
 **Para imprimir o valor de uma variável**  
  
-   No **janela comando**, digite **debug. Print \<variávelname>** e pressione Enter.  
  
 **Para listar informações sobre o thread atual**  
  
-   No **janela comando**, digite `Debug.ListThread`e pressione Enter.  
  
 **Para adicionar uma variável à janela QuickWatch**  
  
-   No **janela comando**, digite **debug. QuickWatch \<VariableName>** e pressione Enter.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](transact-sql-debugger.md)  
