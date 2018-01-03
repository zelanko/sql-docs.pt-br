---
title: Criar consultas UNION (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90517ac0b505592b94d842be81b90ea094633481
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="create-union-queries-visual-database-tools"></a>Criar consultas UNION (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] A palavra-chave UNION permite que se incluam resultados de duas instruções SELECT em uma tabela resultante. Todas as linhas retornadas da instrução SELECT são combinadas no resultado da expressão UNION. Para ver exemplos, consulte [Exemplos de SELECT (Transact-SQL)](http://msdn.microsoft.com/en-us/9b9caa3d-e7d0-42e1-b60b-a5572142186c).  
  
> [!NOTE]  
> O painel Diagrama só pode exibir uma cláusula SELECT. Portanto, ao trabalhar com uma consulta UNION, o Designer de Consulta ocultará o painel Operações da Tabela.  
  
### <a name="to-create-a-merged-select-query"></a>Para criar uma consulta SELECT mesclada  
  
1.  Abra uma consulta ou crie uma nova.  
  
2.  No painel SQL, digite uma expressão UNION válida.  
  
    A seguir, um exemplo de uma expressão UNION válida.  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  No menu do **Designer de Consultas** , clique em **Executar SQL** para executar a consulta.  
  
    Nesse momento, a consulta UNION é formatada pelo Designer de Consulta.  
  
## <a name="see-also"></a>Consulte Também  
[Tipos de consulta permitidos (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Executar operações básicas com consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](http://msdn.microsoft.com/en-us/607c296f-8a6a-49bc-975a-b8d0c0914df7)  
  
