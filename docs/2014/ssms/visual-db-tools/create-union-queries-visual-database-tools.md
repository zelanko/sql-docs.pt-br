---
title: Criar consultas UNION (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fbfe0de4422aba4a73a5cabf16c42566c272a7d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115566"
---
# <a name="create-union-queries-visual-database-tools"></a>Criar consultas UNION (Visual Database Tools)
  A palavra-chave UNION permite que se incluam resultados de duas instruções SELECT em uma tabela resultante. Todas as linhas retornadas da instrução SELECT são combinadas no resultado da expressão UNION. Para obter exemplos, consulte [selecione exemplos &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql).  
  
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
 [Tópicos de instruções de consultas e modos de exibição de design &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Executar operações básicas com consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [União &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/set-operators-union-transact-sql)  
  
  
