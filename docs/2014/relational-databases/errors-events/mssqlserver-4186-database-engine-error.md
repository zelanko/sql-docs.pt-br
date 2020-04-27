---
title: MSSQLSERVER_4186 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4186 (Database Engine error)
ms.assetid: 1ae88554-f291-45bc-a186-6f41d9cd0fca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53a8e0ab728c1fee0033ef86dbf6b7dfc22bdc8c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62867835"
---
# <a name="mssqlserver_4186"></a>MSSQLSERVER_4186
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|4186|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|A coluna '%ls.%.*ls' não pode ser referenciada na cláusula OUTPUT porque a definição da coluna contém uma subconsulta ou faz referência a uma função que executa acesso a dados de sistema ou de usuário. Por padrão, se uma função não estabelece associação com o esquema, supõe-se que ela execute acesso a dados. Considere remover a subconsulta ou a função da definição de coluna ou remover a coluna da cláusula OUTPUT.|  
  
## <a name="explanation"></a>Explicação  
 Para evitar comportamento não determinístico, a cláusula OUTPUT não pode fazer referência a uma coluna de uma exibição ou função com valor de tabela embutida quando essa coluna é definida por um dos seguintes métodos:  
  
-   Uma subconsulta.  
  
-   Uma função definida pelo usuário que executa acesso a dados de usuário ou de sistema ou que supostamente executa tal acesso.  
  
-   Uma coluna computada que contém uma função definida pelo usuário e que executa acesso a dados de usuário ou de sistema em sua definição.  
  
### <a name="examples"></a>Exemplos  
 **Coluna de exibição definida por uma subconsulta**  
  
 O exemplo a seguir cria uma exibição que usa uma subconsulta da lista de seleção para definir a coluna `State`. Uma instrução UPDATE referencia a coluna `State` na cláusula OUTPUT e falha devido à subconsulta na lista de seleção.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.V1  
AS  
    SELECT City,  
-- subquery to return the State name  
           (SELECT Name FROM Person.StateProvince AS sp   
            WHERE sp.StateProvinceID = a.StateProvinceID) AS State  
    FROM Person.Address AS a;  
GO  
--Reference the State column in the OUTPUT clause of an UPDATE statement  
UPDATE dbo.V1   
SET City = City + 'Test'   
OUTPUT deleted.City, deleted.State, inserted.City, inserted.State  
WHERE State = 'Texas';  
GO  
```  
  
 **Coluna de exibição definida por uma função**  
  
 O exemplo a seguir cria uma exibição que usa a função escalar de acesso a dados `dbo.ufnGetStock` na lista de seleção para definir a coluna `CurrentInventory`. Em seguida, uma instrução UPDATE referencia a coluna `CurrentInventory` na cláusula OUTPUT.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ReorderLevels  
AS  
    SELECT ProductID, ProductModelID, ReorderPoint,  
           dbo.ufnGetStock(ProductID) AS CurrentInventory  
    FROM Production.Product;  
GO  
  
UPDATE Production.ReorderLevels  
SET ReorderPoint += CurrentInventory  
OUTPUT deleted.ReorderPoint, deleted.CurrentInventory,  
       inserted.ReorderPoint, inserted.CurrentInventory  
WHERE ProductModelID BETWEEN 75 and 80;  
```  
  
## <a name="user-action"></a>Ação do usuário  
 O erro 4186 pode ser corrigido de uma das seguintes maneiras:  
  
-   Use junções em vez de subconsultas para definir a coluna na exibição ou função. Por exemplo, você pode reescrever a exibição `dbo.V1` da seguinte forma:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE VIEW dbo.V1  
    AS  
        SELECT City, sp.Name AS State  
        FROM Person.Address AS a   
        JOIN Person.StateProvince AS sp   
        ON sp.StateProvinceID = a.StateProvinceID;  
    ```  
  
-   Examine a definição da outra função definida pelo usuário. Se a função não executar acesso a dados de usuário ou de sistema, altere-a para incluir a cláusula WITH SCHEMABINDING.  
  
-   Remova a coluna de cláusula OUTPUT.  
  
## <a name="see-also"></a>Consulte Também  
 [Cláusula OUTPUT &#40;Transact-SQL&#41;](/sql/t-sql/queries/output-clause-transact-sql)  
  
  
