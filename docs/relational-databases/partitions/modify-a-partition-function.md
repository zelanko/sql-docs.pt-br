---
description: Modificar uma função de partição
title: Modificar uma função de partição | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae5bfc09-f27a-4ea9-9518-485278b11674
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2717bf5791cd5f057a57da6693e05700c9045e3c
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88326902"
---
# <a name="modify-a-partition-function"></a>Modificar uma função de partição
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Você pode alterar o modo como uma tabela ou um índice é particionado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] adicionando ou subtraindo o número de partições especificadas, em incrementos de 1, na função de partição da tabela ou do índice particionado usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ao adicionar uma partição, você “divide” em duas uma partição existente e redefine os limites das novas partições. Ao descartar uma partição, você "funde" os limites das duas partições criando uma só. Esta última ação repopula uma partição e deixa a outra partição não atribuída.  
  
> [!CAUTION]  
>  Mais de uma tabela ou índice podem usar a mesma função de partição. Quando modifica uma função de partição, você afeta todas elas em uma única transação. Verifique as dependências da função de partição antes de modificá-la.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para modificar uma função de partição usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   ALTER PARTITION FUNCTION só pode ser usada para dividir uma partição em duas ou para mesclar duas partições em uma. Para alterar a forma como uma tabela ou índice é particionado (por exemplo, de 10 partições em 5), você pode usar qualquer uma das opções a seguir.  
  
    -   Crie uma nova tabela particionada com a função de partição desejada e insira os dados da tabela antiga na nova tabela, usando uma instrução INSERT INTO... A instrução SELECT FROM [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o **Assistente para Gerenciar Partição** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
    -   Crie um índice clusterizado particionado em um heap.  
  
        > [!NOTE]  
        >  Descartando resultados de um índice clusterizado particionado em um heap particionado.  
  
    -   Descarte e recrie um índice particionado existente usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX com a cláusula DROP EXISTING = ON.  
  
    -   Execute uma sequência de instruções ALTER PARTITION FUNCTION.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fornece suporte de replicação para modificar uma função de partição. Se você quiser fazer alterações em uma função de partição no banco de dados de publicação, será preciso fazê-las manualmente no banco de dados de assinatura.  
  
-   Todos os grupos de arquivos afetados por ALTER PARTITION FUNCTION devem estar online.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Qualquer uma das permissões a seguir pode ser usada para executar ALTER PARTITION FUNCTION:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   A permissão CONTROL ou ALTER no banco de dados no qual a função de partição foi criada.  
  
-   A permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual a função de partição foi criada.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para modificar uma função de partição:**  
  
 Essa ação específica não pode ser executada com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para modificar uma função de partição, primeiro você deve excluir a função e depois criar uma nova função com as propriedades desejadas usando o Assistente para Criar Partição. Para obter mais informações, consulte  
  
#### <a name="to-delete-a-partition-function"></a>Para excluir uma função de partição  
  
1.  Expanda o banco de dados no qual você deseja excluir a função de partição e expanda a pasta **Repositório** .  
  
2.  Expanda a pasta **Funções de partição** .  
  
3.  Clique com o botão direito do mouse na função de partição a ser excluída e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objeto** , verifique se a função de partição correta está selecionada e clique em **OK**.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-split-a-single-partition-into-two-partitions"></a>Para dividir uma única partição em duas partições  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Look for a previous version of the partition function "myRangePF1" and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called "myRangePF1" that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Split the partition between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    ```  
  
#### <a name="to-merge-two-partitions-into-one-partition"></a>Para mesclar duas partições em uma partição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Look for a previous version of the partition function "myRangePF1" and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called "myRangePF1" that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Merge the partitions between boundary_values 1 and 100  
    --and between boundary_values 100 and 1000 to create one partition  
    --between boundary_values 1 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    MERGE RANGE (100);  
    ```  
  
 Para obter mais informações, veja [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md).  
  
  
