---
title: Otimizando a tabela NewOrg | Microsoft Docs
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
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6ac25b85afabdeb906005346c349941a49ca8de4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-1-3---optimizing-the-neworg-table"></a>Lição 1-3 – Otimizando a tabela NewOrg
A tabela **NewOrd** criada na tarefa [Populando uma tabela com dados hierárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) contém todas as informações de funcionários e representa a estrutura hierárquica usando um tipo de dados **hierarchyid** . Essa tarefa adiciona índices novos para dar suporte às pesquisas na coluna **hierarchyid** .  
  
## <a name="clustered-index"></a>Índice clusterizado  
A coluna **hierarchyid** (**OrgNode**) é a chave primária da tabela **NewOrg** . Quando a tabela foi criada, ela continha um índice clusterizado chamado **PK_NewOrg_OrgNode** para impor a exclusividade da coluna **OrgNode** . Esse índice clusterizado também oferece suporte a uma pesquisa primária detalhada da tabela.  
  
## <a name="nonclustered-index"></a>Índice não clusterizado  
Este passo cria dois índices não clusterizados para oferecer suporte a pesquisas típicas.  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>Para indexar a tabela NewOrg para pesquisas eficientes  
  
1.  Para ajudar as consultas no mesmo nível na hierarquia, use o método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para criar uma coluna calculada que contém o nível na hierarquia. Em seguida, crie um índice composto no nível e em **Hierarchyid**. Execute o código a seguir para criar a coluna computada e o índice de amplitude primária:  
  
    ```  
    ALTER TABLE NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Crie um índice exclusivo na coluna **EmployeeID** . Esta é uma pesquisa singleton tradicional de um único funcionário pelo número **EmployeeID** . Execute o seguinte código para criar um índice em **EmployeeID**:  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON NewOrg(EmployeeID) ;  
    GO  
    ```  
  
3.  Execute o código a seguir para recuperar dados da tabela na ordem de cada um dos três índices:  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM NewOrg   
    ORDER BY OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY H_Level, OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Compare os conjuntos de resultados para ver como a ordem está armazenada em cada tipo de índice. Seguem apenas as primeiras quatro linhas de cada saída.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    Índice de profundidade primária: os registros de funcionário são armazenados adjacentes aos de seu gerente.  
  
    `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
    `/             0x         0         1      zarifin`  
  
    `/1/          0x58        1         2      tplate`  
  
    `/1/1/       0x5AC0       2         4      schai`  
  
    `/1/1/1/     0x5AD6       3         9      jwang`  
  
    `/1/1/2/     0x5ADA       3        10      malexander`  
  
    `/1/2/       0x5B40       2         5      elang`  
  
    `/1/3/       0x5BC0       2         6      gsmits`  
  
    `/2/         0x68         1         3      hjensen`  
  
    `/2/1/       0x6AC0       2         7      sdavis`  
  
    `/2/2/       0x6B40       2         8      norint`  
  
    Índice de **EmployeeID** primário: as linhas são armazenadas na sequência de **EmployeeID**.  
  
    `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
    `/             0x         0         1      zarifin`  
  
    `/1/          0x58        1         2      tplate`  
  
    `/2/         0x68         1         3      hjensen`  
  
    `/1/1/       0x5AC0       2         4      schai`  
  
    `/1/2/       0x5B40       2         5      elang`  
  
    `/1/3/       0x5BC0       2         6      gsmits`  
  
    `/2/1/       0x6AC0       2         7      sdavis`  
  
    `/2/2/       0x6B40       2         8      norint`  
  
    `/1/1/1/     0x5AD6       3         9      jwang`  
  
    `/1/1/2/     0x5ADA       3        10      malexander`  
  
> [!NOTE]  
> Para diagramas que mostram a diferença entre um índice de profundidade primária e um índice de amplitude primária, consulte [Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
  
#### <a name="to-drop-the-unnecessary-columns"></a>Para cancelar as colunas desnecessárias  
  
1.  A coluna **ManagerID** representa a relação funcionário/gerente, que é representada agora pela coluna **OrgNode** . Se outros aplicativos não precisarem da coluna **ManagerID** , considere removê-la usando a seguinte instrução:  
  
    ```  
    ALTER TABLE NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  A coluna **EmployeeID** também é redundante. A coluna **OrgNode** identifica cada empregado de forma exclusiva. Se os outros aplicativos não precisarem da coluna **EmployeeID** , considere remover o índice e depois a coluna usando o seguinte código:  
  
    ```  
    DROP INDEX EmpIDs_unq ON NewOrg ;  
    ALTER TABLE NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>Para substituir a tabela original pela tabela nova  
  
1.  Se sua tabela original continha outros índices ou restrições, adicione-os à tabela **NewOrg** .  
  
2.  Substitua a tabela antiga **EmployeeDemo** pela nova tabela. Execute o código a seguir para cancelar a tabela antiga e então renomeie a tabela nova com o nome antigo:  
  
    ```  
    DROP TABLE EmployeeDemo ;  
    GO  
    sp_rename 'NewOrg', EmployeeDemo ;  
    GO  
    ```  
  
3.  Execute o código a seguir para examinar a tabela final:  
  
    ```  
    SELECT * FROM EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Resumo: convertendo uma tabela para uma estrutura hierárquica](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
  

