---
title: MSSQLSERVER_207 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 207 (Database Engine error)
ms.assetid: d1ab00c7-0331-437a-84fe-bae53b82feec
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ba320288a06dd8498d9699712a6e53e34ae93c09
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver207"></a>MSSQLSERVER_207
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|207|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQ_BADCOL|  
|Texto da mensagem|Nome de coluna inválido '%.*ls'.|  
  
## <a name="explanation"></a>Explicação  
Esse erro de consulta pode ser provocado por um dos problemas a seguir.  
  
-   O nome da coluna foi digitado incorretamente ou a coluna não existe em nenhuma das tabelas especificadas.  
  
-   O agrupamento do banco de dados diferencia maiúsculas e minúsculas e as maiúsculas e minúsculas do nome da coluna especificado na consulta não correspondem às maiúsculas e minúsculas definidas na tabela. Por exemplo, quando uma coluna estiver definida em uma tabela como **LastName** e o banco de dados usar um agrupamento com diferenciação de maiúsculas e minúsculas, as consultas que fizerem referência à coluna como **Lastname** ou **lastname** retornarão o erro 207, pois o nome da coluna não é correspondente.  
  
-   Um alias de coluna definido na cláusula SELECT é referenciado em outra cláusula, como em uma cláusula WHERE ou GROUP BY. Por exemplo, a consulta a seguir define o alias de coluna `Year` na cláusula SELECT e faz referência a ele na cláusula GROUP BY.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year, SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY Year;  
    ```  
  
    Devido à ordem em que as cláusulas da consulta são processadas logicamente, o exemplo retorna o erro 207. A ordem do processamento é a seguinte:  
  
    1.  FROM  
  
    2.  ON  
  
    3.  JOIN  
  
    4.  WHERE  
  
    5.  GROUP BY  
  
    6.  WITH CUBE ou WITH ROLLUP  
  
    7.  HAVING  
  
    8.  SELECT  
  
    9. DISTINCT  
  
    10. ORDER BY  
  
    11. INÍCIO  
  
    Como um alias de coluna não é definido até que a cláusula SELECT seja processada, o nome do alias é desconhecido quando a cláusula GROUP BY é processada.  
  
-   A instrução MERGE aciona esse erro quando a cláusula *<merge_matched>* referencia colunas na tabela de origem, mas nenhuma linha é retornada pela tabela de origem na cláusula WHEN NOT MATCHED BY SOURCE. O erro ocorre porque as colunas na tabela de origem não podem ser acessadas quando nenhuma linha é retornada para a consulta. Por exemplo, a cláusula `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` poderá fazer com que a instrução falhe se `Col1` estiver inacessível na tabela de origem.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique as informações a seguir e corrija a instrução conforme apropriado.  
  
-   O nome da coluna existe na tabela e está digitado corretamente. O exemplo a seguir consulta a exibição do catálogo **sys.columns** para retornar todos os nomes de colunas de determinada tabela.  
  
    ```  
    SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('schema_name.table_name');  
    ```  
  
-   A diferenciação de maiúsculas e minúsculas do agrupamento de banco de dados. A instrução a seguir retorna o agrupamento do banco de dados especificado.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    A abreviação CS no nome do agrupamento indica que ele diferencia maiúsculas de minúsculas. Por exemplo, Latin1_General_CS_AS é um agrupamento que tem diferenciação de maiúsculas e minúsculas e de acentos. Modifique o nome da coluna para que coincida com as maiúsculas e minúsculas do nome da coluna conforme definido na tabela.  
  
-   O alias de uma coluna está referenciado incorretamente. Modifique a instrução repetindo a expressão que define o alias na cláusula adequada ou usando uma tabela derivada. O exemplo a seguir repete as expressões que definem o alias `Year` na cláusula GROUP BY.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year ,SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY DATEPART(yyyy,OrderDate);  
    ```  
  
    O exemplo a seguir usa uma tabela derivada para disponibilizar o nome do alias para outras cláusulas na consulta. Observe que o alias `Year` está definido na cláusula FROM que é processada primeiro e, portanto, disponibiliza o alias para uso em outras cláusulas na consulta.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT d.Year, SUM(TotalDue) AS Total  
    FROM (SELECT DATEPART(yyyy,OrderDate) AS Year, TotalDue  
          FROM Sales.SalesOrderHeader)AS d  
    GROUP BY Year;  
    ```  
  
-   A cláusula WHEN NOT MATCHED BY SOURCE na instrução MERGE faz referência a um valor que pode ser acessado. Modifique a instrução MERGE de forma que pelo menos uma linha seja retornada pela tabela de origem na cláusula WHEN NOT MATCHED BY SOURCE. Por exemplo, talvez você precise adicionar ou revisar a condição da pesquisa especificada para a cláusula. Como alternativa, é possível modificar a cláusula para especificar um valor que não faz referência à tabela de origem. Por exemplo, `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = <expression, or other available value>`.  
  
## <a name="see-also"></a>Consulte também  
[MERGE &#40;Transact-SQL&#41;](~/t-sql/statements/merge-transact-sql.md)  
[FROM &#40;Transact-SQL&#41;](~/t-sql/queries/from-transact-sql.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
  

