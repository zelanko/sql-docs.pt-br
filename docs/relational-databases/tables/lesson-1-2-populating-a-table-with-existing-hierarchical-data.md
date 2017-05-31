---
title: "Populando uma tabela com os dados hierárquicos existentes | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: fd943d84-dbe6-4a05-912b-c88164998d80
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4569fb3f5bc56d04624756eb3fccba8da1d4ad2f
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-2---populating-a-table-with-existing-hierarchical-data"></a>Lição 1-2 – Populando uma tabela com os dados hierárquicos existentes
Essa tarefa cria uma tabela nova e a popula com os dados da tabela **EmployeeDemo** . Essa tarefa tem as seguintes etapas:  
  
-   Crie uma nova tabela que contém uma coluna **hierarchyid** . Essa coluna pode substituir as colunas **EmployeeID** e **ManagerID** existentes. Entretanto, você manterá essas colunas. Isso porque os aplicativos existentes podem se referir a essas colunas e, também, para ajudar a compreender os dados depois da transferência. A definição da tabela especifica que **OrgNode** é a chave primária, exigindo que a coluna contenha valores exclusivos. O índice clusterizado da coluna **OrgNode** armazenará a data na sequência **OrgNode** .  
  
-   Crie uma tabela temporária que será usada para localizar quantos funcionários se reportam diretamente a cada gerenciador.  
  
-   Popule a nova tabela usando dados da tabela **EmployeeDemo** .  
  
### <a name="to-create-a-new-table-named-neworg"></a>Para criar uma tabela chamada NewOrg  
  
-   Em uma janela do Editor de Consultas, execute o seguinte código para criar uma tabela chamada **HumanResources.NewOrg**:  
  
    ```  
    CREATE TABLE NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="to-create-a-temporary-table-named-children"></a>Para criar uma tabela temporária chamada #Children  
  
1.  Crie uma tabela temporária chamada **#Children** com uma coluna chamada **Num** que conterá o número de filhos de cada nó:  
  
    ```  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  Adicione um índice que acelerará consideravelmente a consulta que popula a tabela **NewOrg** :  
  
    ```  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="to-populate-the-neworg-table"></a>Para popular a tabela NewOrg  
  
1.  Consultas recursivas proíbem subconsultas com agregações. Em vez disso, popule a tabela **#Children** com o seguinte código, que usa o método [ROW_NUMBER()](../../t-sql/functions/row-number-transact-sql.md) para popular a coluna **Num** :  
  
    ```  
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM EmployeeDemo  
    GO  
  
    ```  
  
2.  Examine a tabela **#Children** . Observe como a coluna **Num** contém números sequenciais para cada gerenciador.  
  
    ```  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    `EmployeeID ManagerID Num`  
  
    `---------- --------- ---`  
  
    `1        NULL       1`  
  
    `2         1         1`  
  
    `3         1         2`  
  
    `4         2         1`  
  
    `5         2         2`  
  
    `6         2         3`  
  
    `7         3         1`  
  
    `8         3         2`  
  
    `9         4         1`  
  
    `10        4         2`  
  
3.  Popule a tabela **NewOrg** . Use os métodos GetRoot e ToString para concatenar os valores **Num** no formato **hierarchyid** e atualize a coluna **OrgNode** com os valores hierárquicos resultantes:  
  
    ```  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   
  
    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO  
  
    ```  
  
4.  Uma coluna **hierarchyid** fica mais fácil de entender quando você a converte no formato de caractere. Examine os dados da tabela **NewOrg** executando o seguinte código, que contém duas representações da coluna **OrgNode** :  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM NewOrg   
    ORDER BY LogicalNode;  
    GO  
  
    ```  
  
    A coluna **LogicalNode** converte a coluna **hierarchyid** em um formulário de texto mais legível que representa a hierarquia. Nas tarefas restantes, você usará o método `ToString()` para mostrar o formato lógico das colunas **hierarchyid** .  
  
5.  Descarte a tabela temporária, que não será mais necessária:  
  
    ```  
    DROP TABLE #Children  
    GO  
    ```  
  
A próxima tarefa criará índices para oferecer suporte à estrutura hierárquica.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Otimizando a tabela NewOrg](../../relational-databases/tables/lesson-1-3-optimizing-the-neworg-table.md)  
  
  
  

