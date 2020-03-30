---
title: 'Lição 2: Criando e gerenciando dados em uma tabela hierárquica | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 95f55cff-4abb-4c08-97b3-e3ae5e8b24e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 657dedcf4944a2540d1237b53fa8ea822c31ae3f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68031638"
---
# <a name="lesson-2-create-and-manage-data-in-a-hierarchical-table"></a>Lição 2: criar e gerenciar dados em uma tabela hierárquica
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Na Lição 1, você modificou uma tabela existente para usar o tipo de dados **hierarchyid** e populou a coluna **hierarchyid** com a representação dos dados existentes. Nesta lição, você iniciará com uma tabela nova, e inserindo dados usando os métodos hierárquicos. Em seguida, você vai consultar e manipular os dados usando os métodos hierárquicos. 

## <a name="prerequisites"></a>Prerequisites  
Para concluir este tutorial, você precisará do SQL Server Management Studio, bem como acesso a um servidor que executa o SQL Server e um banco de dados do AdventureWorks.

- Instale o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Baixe o [Bancos de dados de exemplo do AdventureWorks2017](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).

As instruções para restaurar bancos de dados no SSMS são encontradas aqui: [Restaurando um banco de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).   
  
## <a name="create-a-table-using-the-hierarchyid-data-type"></a>Criar uma tabela por meio de um tipo de dados hierarchyid
O exemplo a seguir cria uma tabela com o nome EmployeeOrg, que inclui dados de funcionário junto com sua hierarquia de relatórios. O exemplo cria a tabela no banco de dados AdventureWorks2017, mas isso é opcional. Para manter o exemplo simples, essa tabela inclui somente cinco colunas:  
  
-   OrgNode é uma coluna **hierarchyid** que armazena a relação hierárquica.   
-   OrgLevel é uma coluna computada, com base na coluna OrgNode, que armazena cada nível de nó na hierarquia. Ela será usada para um índice por amplitude.  
-   EmployeeID contém o número de identificação de funcionário comum usado para aplicativos como folha de pagamento. No desenvolvimento de um novo aplicativo, os aplicativos podem usar a coluna OrgNode e a coluna EmployeeID separada não é necessária.   
-   EmpName contém o nome do funcionário.    
-   Title contém o cargo do funcionário.  

## <a name="create-the-employeeorg-table"></a>Criar a tabela EmployeeOrg  
  
1.  Em uma janela do Editor de Consulta, execute o código a seguir para criar a tabela `EmployeeOrg` . A especificação da coluna `OrgNode` como a chave primária com um índice clusterizado criará um índice por amplitude:  
  
    ```sql  
    USE AdventureWorks2017 ;  
    GO  
    
    if OBJECT_ID('HumanResources.EmployeeOrg') is not null
     drop table HumanResources.EmployeeOrg 
         
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  Execute o seguinte código para criar um índice composto nas colunas `OrgLevel` e `OrgNode` para oferecer suporte a pesquisas eficientes por amplitude:  
  
    ```sql  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
Agora a tabela está pronta para receber dados. A próxima tarefa populará a tabela usando métodos hierárquicos.   

## <a name="populate-a-hierarchical-table-using-hierarchical-methods"></a>Preencher uma tabela hierárquica utilizando métodos hierárquicos
O AdventureWorks2017 tem oito funcionários que trabalham no departamento de Marketing. A hierarquia dos funcionários é assim:  
  
**Davi**, **EmployeeID** 6, é o Gerente de Marketing. Três especialistas em Marketing são subordinados a **Davi**:  
  
-   **Sara**, **EmployeeID** 46  
  
-   **Bruno**, **EmployeeID** 271  
  
-   **Julieta**, **EmployeeID** 119  
  
A Assistente de Marketing **Valentina** , (**EmployeeID** 269), é subordinada a **Sara**, e a Assistente de Marketing **Marina** , (**EmployeeID** 272), é subordinada a **Bruno**.  
  
### <a name="insert-the-root-of-the-hierarchy-tree"></a>Inserir a raiz da árvore de hierarquia  
  
1.  O exemplo a seguir insere **Davi** , o Gerente de Marketing, na tabela da raiz da hierarquia. A coluna **OrdLevel** é uma coluna calculada. Portanto, não faz parte da instrução INSERT. Este primeiro registro usa o método [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) para popular o primeiro registro como a raiz da hierarquia.  
  
    ```sql  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  Execute o seguinte código para examinar a linha inicial na tabela:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
Como na lição anterior, usamos o método `ToString()` para converter o tipo de dados **hierarchyid** em um formato mais fácil de entender.  
  
### <a name="insert-a-subordinate-employee"></a>Inserir um funcionário subordinado  
  
1.  **Sara** é subordinada a **Davi**. Para inserir o nó de **Sara** , você deve criar um valor **OrgNode** apropriado do tipo de dados **hierarchyid**. O código a seguir cria uma variável do tipo de dados **hierarchyid** e a popula com o valor OrgNode de raiz da tabela. Em seguida, usa essa variável com o método [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) para inserir a linha que é um nó subordinado. `GetDescendant` usa dois argumentos. Analise as seguintes opções para os valores de argumento:  
  
    -   Se o pai for o NULL, o `GetDescendant` retornará NULL.  
    -   Se o pai não for NULL, e child1 e child2 forem NULL, o `GetDescendant` retornará um filho de pai.  
    -   Se o pai e child1 forem NULL e child2 for NULL, o `GetDescendant` retornará um filho de pai maior que child1.   
    -   Se o pai e child2 não forem NULL e child1 for NULL, o `GetDescendant` retornará um filho de pai menor que child2.   
    -   Se o pai, child 1 e child 2 não forem NULL, o `GetDescendant` retornará um filho de pai maior que child1 e menor que child2.  
  
    O código a seguir usa os argumentos `(NULL, NULL)` do pai da raiz, pois ainda não há linhas na tabela exceto a raiz. Execute o seguinte código para inserir **Sara**:  
  
    ```sql  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  Repita a consulta do primeiro procedimento para consultar a tabela e verificar como as entradas são exibidas:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="create-a-procedure-for-entering-new-nodes"></a>Criar um procedimento para inserir novos nós  
  
1.  Para simplificar a inserção de dados, crie o procedimento armazenado a seguir para adicionar funcionários à tabela **EmployeeOrg** . O procedimento aceita valores de entrada sobre o empregado sendo adicionado. Isso inclui o **EmployeeID** do gerente do novo funcionário, o número **EmployeeID** do novo funcionário, além de seu nome e cargo. O procedimento usa `GetDescendant()` e o método [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) . Execute o seguinte código para criar o procedimento:  
  
    ```sql  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  O exemplo a seguir adiciona os quatro funcionários restantes que são subordinados direta ou indiretamente a **Davi**.  
  
    ```sql  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  Novamente, execute a seguinte consulta para examinar as linhas na tabela **EmployeeOrg** :  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    /1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
Agora a tabela está totalmente populada com a organização de marketing.  

## <a name="query-a-hierarchical-table-using-hierarchy-methods"></a>Consultar uma tabela hierárquica por meio de métodos de hierarquia
Agora que a tabela HumanResources.EmployeeOrg está completamente populada, essa tarefa mostrará como consultar a hierarquia usando alguns métodos hierárquicos.  
  
### <a name="find-subordinate-nodes"></a>Localizar nós subordinados  
  
1.  Sariya tem um funcionário subordinado. Para consultar os subordinados de Sara, execute a seguinte consulta, que usa o método [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) :  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    O resultado lista Sariya e Wanida. Sariya é listada porque é a descendente no nível 0. Wanida é a descendente no nível 1.  
  
2.  Você também pode consultar essas informações usando o método [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) . `GetAncestor` usa um argumento para o nível que você está tentando retornar. Como Wanida está um nível abaixo de Sariya, use `GetAncestor(1)` conforme demonstrado no seguinte código:  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
    Desta vez o resultado lista apenas Wanida.  
  
3.  Agora altere o `@CurrentEmployee` para David (EmployeeID 6) e o nível para 2. Execute o seguinte para retornar também Wanida:  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    Desta vez, você também recebe Mary que também é subordinada a David, dois níveis abaixo.  
  
## <a name="use-getroot-and-getlevel"></a>Usar GetRoot e GetLevel  
  
1.  À medida que a hierarquia fica maior é mais difícil determinar onde os membros estão na hierarquia. Use o método [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) para localizar quantos níveis abaixo cada linha está na hierarquia. Execute o seguinte código para exibir os níveis de todas as linhas:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  Use o método [GetRoot](../../t-sql/data-types/getroot-database-engine.md) para localizar o nó raiz na hierarquia. O seguinte código retorna uma única linha que é a raiz:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
   
  
## <a name="reorder-data-in-a-hierarchical-table-using-hierarchical-methods"></a>Reordenar dados em tabela hierárquica por meio de métodos hierárquicos
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Reorganizar uma hierarquia é uma tarefa de manutenção comum. Nesta tarefa, usaremos a instrução UPDATE com o método [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) para mover primeiramente uma única linha para um novo local da hierarquia. Em seguida, moveremos uma subárvore inteira para um novo local.  
  
O método `GetReparentedValue` toma dois argumentos. O primeiro argumento descreve a parte da hierarquia a ser modificada. Por exemplo, se uma hierarquia for **/1/4/2/3/** e você desejar alterar a seção **/1/4/** , a hierarquia se tornará **/2/1/2/3/** ; se deixar os últimos dois nós (**2/3/** ) inalterados, você precisará fornecer os nós que estão sendo alterados ( **/1/4/** ) como o primeiro argumento. O segundo argumento fornece o novo nível hierárquico, em nosso exemplo **/2/1/** . Os dois argumentos não precisam conter o mesmo número de níveis.  
  
### <a name="move-a-single-row-to-a-new-location-in-the-hierarchy"></a>Mover uma linha única para um novo local hierárquico  
  
1.  Atualmente, Wanida reporta-se a Sariya. Neste procedimento, você move Valentina de seu nó **/1/1/** atual, de modo que ela se reporte a Julieta. Seu novo nó se tornará **/3/1/** e, dessa forma, **/1/** será o primeiro argumento e **/3/** o segundo. Esses correspondem aos valores **OrgNode** de Sara e Julieta. Execute o código a seguir para mover Wanida da organização de Sariya para a organização de Jill:  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 269 ;   
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 46 ;   
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 119 ;   
  
    UPDATE HumanResources.EmployeeOrg  
    SET OrgNode = @CurrentEmployee. GetReparentedValue(@OldParent, @NewParent)   
    WHERE OrgNode = @CurrentEmployee ;  
    GO  
    ```  
  
2.  Execute o seguinte código para ver o resultado:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    Valentina encontra-se agora no nó **/3/1/** .  
  
### <a name="reorganize-a-section-of-a-hierarchy"></a>Reorganizar uma seção de hierarquia  
  
1.  Para demonstrar como mover um grande número de pessoas ao mesmo tempo, execute primeiramente o código a seguir para adicionar um estagiário se reportando a Wanida:  
  
    ```sql  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  Kevin agora se reporta a Wanida, que se reporta a Jill, que se reporta a David. Isso significa que Julio se encontra no nível **/3/1/1/** . Para mover todos os subordinados de Julieta para um novo administrador, atualizaremos todos os nós com **/3/** como seus **OrgNode** para um novo valor. Execute o seguinte código para atualizar Wanida, de modo que passe a se reportar a Sariya, mas deixando Kevin se reportando a Wanida:  
  
    ```sql  
    DECLARE @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 119 ; -- Jill  
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ; -- Sariya  
    DECLARE children_cursor CURSOR FOR  
    SELECT OrgNode FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @OldParent;  
    DECLARE @ChildId hierarchyid;  
    OPEN children_cursor  
    FETCH NEXT FROM children_cursor INTO @ChildId;  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
    START:  
        DECLARE @NewId hierarchyid;  
        SELECT @NewId = @NewParent.GetDescendant(MAX(OrgNode), NULL)  
        FROM HumanResources.EmployeeOrg WHERE OrgNode.GetAncestor(1) = @NewParent;  
  
        UPDATE HumanResources.EmployeeOrg  
        SET OrgNode = OrgNode.GetReparentedValue(@ChildId, @NewId)  
        WHERE OrgNode.IsDescendantOf(@ChildId) = 1;  
        IF @@error <> 0 GOTO START -- On error, retry  
            FETCH NEXT FROM children_cursor INTO @ChildId;  
    END  
    CLOSE children_cursor;  
    DEALLOCATE children_cursor;  
  
    ```  
  
3.  Execute o seguinte código para ver o resultado:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
------------ ------- -------- ---------- ------- -----------------  
/            Ox      0        6          David   Marketing Manager  
/1/          0x58    1        46         Sariya  Marketing Specialist  
/1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
/1/1/1/      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
Toda a árvore organizacional que se reportava a Jill (Wanida e Kevin), agora se reporta a Sariya.  
  
Para ver um procedimento armazenado que reorganiza uma seção de uma hierarquia, consulte a seção “Movendo subárvores” de [Movendo subárvores](../../relational-databases/hierarchical-data-sql-server.md#BKMK_MovingSubtrees).  
  
