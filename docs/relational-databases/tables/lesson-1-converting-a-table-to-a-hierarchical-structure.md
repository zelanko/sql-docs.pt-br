---
description: 'Lição 1: conversão de uma tabela em uma estrutura hierárquica'
title: 'Lição 1: Convertendo uma tabela em uma estrutura hierárquica | Microsoft Docs'
ms.custom: ''
ms.date: 08/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4a56b34301386287ef954edae0528decd4d03fee
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91809472"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>Lição 1: conversão de uma tabela em uma estrutura hierárquica
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Os clientes que possuem tabelas que usam autojunções para expressar relações hierárquicas podem converter as tabelas em uma estrutura hierárquica usando esta lição como guia. É relativamente fácil fazer a migração dessa representação para outra usando **hierarchyid**. Depois da migração, os usuários terão uma representação hierárquica compacta e fácil de entender, que poderá ser indexada de várias formas para proporcionar consultas eficientes.  
  
Esta lição examina uma tabela existente, cria uma tabela contendo uma coluna **hierarchyid** , popula a tabela com os dados da tabela de origem e, depois, demonstra três estratégias de indexação. Eis os tópicos desta lição:  
 
  
## <a name="prerequisites"></a>Pré-requisitos  
Para concluir este tutorial, você precisará do SQL Server Management Studio, bem como acesso a um servidor que executa o SQL Server e um banco de dados do AdventureWorks.

- Instale o [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Baixe o [Bancos de dados de exemplo do AdventureWorks2017](../../samples/adventureworks-install-configure.md).

Instruções para restaurar bancos de dados no SSMS são encontradas aqui: [Restaurar um banco de dados](../backup-restore/restore-a-database-backup-using-ssms.md).  

## <a name="examine-the-current-structure-of-the-employee-table"></a>Examinar a estrutura atual da tabela Employee
O banco de dados Adventureworks2017 (ou posterior) de exemplo contém uma tabela **Employee** no esquema **HumanResources**. Para evitar alterar a tabela original, este passo cria uma cópia da tabela **Employee** nomeada **EmployeeDemo**. Para simplificar o exemplo, você copia só cinco colunas da tabela original. Então, você consulta a tabela **HumanResources.EmployeeDemo** para revisar como os dados são estruturados em uma tabela sem usar o tipo de dados **hierarchyid** .  
  
### <a name="copy-the-employee-table"></a>Copiar a tabela Employee  
  
1.  Em uma janela Editor de Consultas, execute o código seguinte para copiar a estrutura de tabela e dados da tabela **Employee** em uma tabela nova nomeada **EmployeeDemo**. Como a tabela original já usa hierarchyid, essa consulta basicamente mescla a hierarquia para recuperar o gerente do funcionário. Em partes subsequentes desta lição, reconstruiremos essa hierarquia.

   ```sql  
   USE AdventureWorks2017;  
   GO  
     if OBJECT_ID('HumanResources.EmployeeDemo') is not null
    drop table HumanResources.EmployeeDemo 

    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
     (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
        WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
            (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID,
          emp.JobTitle, emp.HireDate
   INTO HumanResources.EmployeeDemo   
   FROM HumanResources.Employee emp ;
   GO
   ```  
  
### <a name="examine-the-structure-and-data-of-the-employeedemo-table"></a>Examine a estrutura e os dados da tabela EmployeeDemo  
  
-   Esta nova tabela **EmployeeDemo** representa uma tabela típica em um banco de dados existente que você pode querer migrar para uma nova estrutura. Em uma janela de Editor de Consultas, execute o código seguinte para mostrar como a tabela usa uma autojunção para exibir as relações de funcionário/gerente:  
  
    ```sql  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL                    1   adventure-works\ken0        Chief Executive Officer
    1   adventure-works\ken0        2   adventure-works\terri0      Vice President of Engineering
    1   adventure-works\ken0       16   adventure-works\david0    Marketing Manager
    1   adventure-works\ken0       25   adventure-works\james1    Vice President of Production
    1   adventure-works\ken0      234   adventure-works\laura1    Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0       Information Services Manager
    1   adventure-works\ken0      273   adventure-works\brian3    Vice President of Sales
    2   adventure-works\terri0    3 adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0        Senior Tool Designer
    ...  
    ```  
  
    Os resultados continuam por um total de 290 linhas.  
  
Observe que a cláusula **ORDER BY** fez com que a saída listasse os relatórios diretos de cada nível de administração junto. Por exemplo, todos os sete relatórios diretos de **MgrID** 1 (ken0) estão listados adjacentes uns aos outros. Embora não seja impossível, é muito mais difícil agrupar todos aqueles que eventualmente se reportem ao **MgrID** 1.  


## <a name="populate-a-table-with-existing-hierarchical-data"></a>Popular uma tabela com os dados hierárquicos existentes
 Essa tarefa cria uma tabela nova e a popula com os dados da tabela **EmployeeDemo**. Essa tarefa tem as seguintes etapas:  
  
-   Crie uma nova tabela que contém uma coluna **hierarchyid** . Essa coluna pode substituir as colunas **EmployeeID** e **ManagerID** existentes. Entretanto, você manterá essas colunas. Isso porque os aplicativos existentes podem se referir a essas colunas e, também, para ajudar a compreender os dados depois da transferência. A definição da tabela especifica que **OrgNode** é a chave primária, exigindo que a coluna contenha valores exclusivos. O índice clusterizado da coluna **OrgNode** armazenará a data na sequência **OrgNode** .    
-   Crie uma tabela temporária que será usada para localizar quantos funcionários se reportam diretamente a cada gerenciador. 
-   Popule a nova tabela usando dados da tabela **EmployeeDemo** .  
  
### <a name="to-create-a-new-table-named-neworg"></a>Para criar uma tabela chamada NewOrg  
  
-   Em uma janela do Editor de Consultas, execute o seguinte código para criar uma tabela chamada **HumanResources.NewOrg**:  
  
    ```sql   
    CREATE TABLE HumanResources.NewOrg  
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
  
### <a name="create-a-temporary-table-named-children"></a>Criar uma tabela temporária chamada #Children  
  
1.  Crie uma tabela temporária chamada **#Children** com uma coluna chamada **Num** que conterá o número de filhos de cada nó:  
  
    ```sql  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  Adicione um índice que acelerará consideravelmente a consulta que popula a tabela **NewOrg** :  
  
    ```sql  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="populate-the-neworg-table"></a>Popular a tabela NewOrg  
  
1.  Consultas recursivas proíbem subconsultas com agregações. Em vez disso, popule a tabela **#Children** com o seguinte código, que usa o método [ROW_NUMBER()](../../t-sql/functions/row-number-transact-sql.md) para popular a coluna **Num** :  
  
    ```sql 
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM HumanResources.EmployeeDemo  
    GO 
    ```  
  
2.  Examine a tabela **#Children** . Observe como a coluna **Num** contém números sequenciais para cada gerenciador.  
  
    ```sql  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

    ```
    EmployeeID  ManagerID   Num
    1   NULL    1
    2        1    1
    16     1      2
    25     1      3
    234    1      4
    263    1      5
    273    1      6
    3        2    1
    4        3    1
    5        3    2
    6        3    3
    7        3    4
    ```


3.  Popule a tabela **NewOrg** . Use os métodos GetRoot e ToString para concatenar os valores **Num** no formato **hierarchyid** e atualize a coluna **OrgNode** com os valores hierárquicos resultantes:  
  
    ```sql  
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
    INSERT HumanResources.NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM HumanResources.EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO 
    ```  
  
4.  Uma coluna **hierarchyid** fica mais fácil de entender quando você a converte no formato de caractere. Examine os dados da tabela **NewOrg** executando o seguinte código, que contém duas representações da coluna **OrgNode** :  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM HumanResources.NewOrg   
    ORDER BY LogicalNode;  
    GO  
    ```  
  
    A coluna **LogicalNode** converte a coluna **hierarchyid** em um formulário de texto mais legível que representa a hierarquia. Nas tarefas restantes, você usará o método `ToString()` para mostrar o formato lógico das colunas **hierarchyid** .  
  
5.  Descarte a tabela temporária, que não será mais necessária:  
  
    ```sql  
    DROP TABLE #Children  
    GO  
    ```  
  
## <a name="optimizing-the-neworg-table"></a>Otimizando a tabela NewOrg
A tabela **NewOrd** criada na tarefa [Populando uma tabela com dados hierárquicos existentes]() contém todas as informações de funcionários e representa a estrutura hierárquica usando um tipo de dados **hierarchyid** . Essa tarefa adiciona índices novos para dar suporte às pesquisas na coluna **hierarchyid** .  
  

A coluna **hierarchyid** (**OrgNode**) é a chave primária da tabela **NewOrg** . Quando a tabela foi criada, ela continha um índice clusterizado chamado **PK_NewOrg_OrgNode** para impor a exclusividade da coluna **OrgNode** . Esse índice clusterizado também oferece suporte a uma pesquisa primária detalhada da tabela.  
  
  
### <a name="create-index-on-neworg-table-for-efficient-searches"></a>Criar índice na tabela NewOrg para pesquisas eficientes  
  
1.  Para ajudar as consultas no mesmo nível na hierarquia, use o método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para criar uma coluna calculada que contém o nível na hierarquia. Em seguida, crie um índice composto no nível e em **Hierarchyid**. Execute o código a seguir para criar a coluna computada e o índice de amplitude primária:  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Crie um índice exclusivo na coluna **EmployeeID** . Esta é uma pesquisa singleton tradicional de um único funcionário pelo número **EmployeeID** . Execute o seguinte código para criar um índice em **EmployeeID**:  
  
    ```sql  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  Execute o código a seguir para recuperar dados da tabela na ordem de cada um dos três índices:  
  
    ```sql  
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

    Índice de **EmployeeID** primário: as linhas são armazenadas na sequência de **EmployeeID** .  

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
  
### <a name="drop-the-unnecessary-columns"></a>Remover as colunas desnecessárias  
  
1.  A coluna **ManagerID** representa a relação funcionário/gerente, que é representada agora pela coluna **OrgNode** . Se outros aplicativos não precisarem da coluna **ManagerID** , considere removê-la usando a seguinte instrução:  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  A coluna **EmployeeID** também é redundante. A coluna **OrgNode** identifica cada empregado de forma exclusiva. Se os outros aplicativos não precisarem da coluna **EmployeeID** , considere remover o índice e depois a coluna usando o seguinte código:  
  
    ```sql  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
### <a name="replace-the-original-table-with-the-new-table"></a>Substituir a tabela original pela nova  
  
1.  Se sua tabela original continha outros índices ou restrições, adicione-os à tabela **NewOrg** .  
  
2.  Substitua a tabela antiga **EmployeeDemo** pela nova tabela. Execute o código a seguir para cancelar a tabela antiga e então renomeie a tabela nova com o nome antigo:  
  
    ```sql  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  Execute o código a seguir para examinar a tabela final:  
  
    ```sql  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-steps"></a>Próximas etapas
O próximo artigo ensina a criar e gerenciar dados em uma tabela hierárquica. 

Vá até o próximo artigo para saber mais:
> [!div class="nextstepaction"]
> [Próximas etapas](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)