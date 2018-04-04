---
title: Otimizando a tabela NewOrg | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39a6587d88d14f9ac1950f7e1f6896258860b452
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="lesson-1-3---optimizing-the-neworg-table"></a>Lição 1-3 – Otimizando a tabela NewOrg
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
A tabela **NewOrd** criada na tarefa [Populando uma tabela com dados hierárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) contém todas as informações de funcionários e representa a estrutura hierárquica usando um tipo de dados **hierarchyid** . Essa tarefa adiciona índices novos para dar suporte às pesquisas na coluna **hierarchyid** .  
  
## <a name="clustered-index"></a>Índice clusterizado  
A coluna **hierarchyid** (**OrgNode**) é a chave primária da tabela **NewOrg** . Quando a tabela foi criada, ela continha um índice clusterizado chamado **PK_NewOrg_OrgNode** para impor a exclusividade da coluna **OrgNode** . Esse índice clusterizado também oferece suporte a uma pesquisa primária detalhada da tabela.  
  
## <a name="nonclustered-index"></a>Índice não clusterizado  
Este passo cria dois índices não clusterizados para oferecer suporte a pesquisas típicas.  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>Para indexar a tabela NewOrg para pesquisas eficientes  
  
1.  Para ajudar as consultas no mesmo nível na hierarquia, use o método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para criar uma coluna calculada que contém o nível na hierarquia. Em seguida, crie um índice composto no nível e em **Hierarchyid**. Execute o código a seguir para criar a coluna computada e o índice de amplitude primária:  
  
    ```  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Crie um índice exclusivo na coluna **EmployeeID** . Esta é uma pesquisa singleton tradicional de um único funcionário pelo número **EmployeeID** . Execute o seguinte código para criar um índice em **EmployeeID**:  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  Execute o código a seguir para recuperar dados da tabela na ordem de cada um dos três índices:  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Compare os conjuntos de resultados para ver como a ordem está armazenada em cada tipo de índice. Seguem apenas as primeiras quatro linhas de cada saída.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    Índice de profundidade primária: os registros de funcionário são armazenados adjacentes aos de seu gerente.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    Índice de **EmployeeID** primário: as linhas são armazenadas na sequência de **EmployeeID**.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> Para diagramas que mostram a diferença entre um índice de profundidade primária e um índice de amplitude primária, consulte [Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
  
#### <a name="to-drop-the-unnecessary-columns"></a>Para cancelar as colunas desnecessárias  
  
1.  A coluna **ManagerID** representa a relação funcionário/gerente, que é representada agora pela coluna **OrgNode** . Se outros aplicativos não precisarem da coluna **ManagerID** , considere removê-la usando a seguinte instrução:  
  
    ```  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  A coluna **EmployeeID** também é redundante. A coluna **OrgNode** identifica cada empregado de forma exclusiva. Se os outros aplicativos não precisarem da coluna **EmployeeID** , considere remover o índice e depois a coluna usando o seguinte código:  
  
    ```  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>Para substituir a tabela original pela tabela nova  
  
1.  Se sua tabela original continha outros índices ou restrições, adicione-os à tabela **NewOrg** .  
  
2.  Substitua a tabela antiga **EmployeeDemo** pela nova tabela. Execute o código a seguir para cancelar a tabela antiga e então renomeie a tabela nova com o nome antigo:  
  
    ```  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  Execute o código a seguir para examinar a tabela final:  
  
    ```  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Resumo: convertendo uma tabela para uma estrutura hierárquica](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
  
