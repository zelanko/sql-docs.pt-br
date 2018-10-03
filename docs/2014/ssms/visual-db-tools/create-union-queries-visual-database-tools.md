---
title: Criar consultas UNION (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5571494e5dbf3410152d18445d4454d91ae8e0d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065798"
---
# <a name="create-union-queries-visual-database-tools"></a>Criar consultas UNION (Visual Database Tools)
  A palavra-chave UNION permite que se incluam resultados de duas instruções SELECT em uma tabela resultante. Todas as linhas retornadas da instrução SELECT são combinadas no resultado da expressão UNION. Para obter exemplos, consulte [exemplos de SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql).  
  
> [!NOTE]  
>  O painel Diagrama só pode exibir uma cláusula SELECT. Portanto, ao trabalhar com uma consulta UNION, o Designer de Consulta ocultará o painel Operações da Tabela.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Suporte para tipos de consulta &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Tópicos explicativos de consultas e exibições de design &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [União &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/set-operators-union-transact-sql)  
  
  
