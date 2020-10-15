---
description: Criar consultas UNION (Visual Database Tools)
title: Criar consultas UNION
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b6d4d7618b3130e2b06d3efb8e9e2a35bc7ca0ee
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038369"
---
# <a name="create-union-queries-visual-database-tools"></a>Criar consultas UNION (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
A palavra-chave UNION permite que se incluam resultados de duas instruções SELECT em uma tabela resultante. Todas as linhas retornadas da instrução SELECT são combinadas no resultado da expressão UNION. Para ver exemplos, consulte [Exemplos de SELECT (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md).  
  
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
[Tipos de Consulta com Suporte](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Executar operações básicas com consultas](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](../../t-sql/language-elements/set-operators-union-transact-sql.md)