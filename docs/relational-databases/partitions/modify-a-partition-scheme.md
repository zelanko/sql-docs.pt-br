---
title: Modificar um esquema de partição | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 515de63f-dfc5-434d-9adb-f3b5992f745a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fb636d8afd8130f9ca4dca5996f5b7226edec7d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207996"
---
# <a name="modify-a-partition-scheme"></a>Modificar um esquema de partição
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode Modificar um esquema de partição no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ao designar um grupo de arquivos para manter a partição seguinte que será adicionada à tabela particionada usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Isso é feito ao atribuir a propriedade NEXT USED a um grupo de arquivos. Você pode atribuir a propriedade NEXT USED a um grupo de arquivos vazio ou para um que já mantenha uma partição. Em outras palavras, um grupo de arquivos pode manter mais de uma partição.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma tabela ou um índice particionado usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Qualquer grupo de arquivos afetado por ALTER PARTITION SCHEME deve estar online.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 As seguintes permissões podem ser usadas para executar ALTER PARTITION SCHEME:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   Permissão CONTROL ou ALTER no banco de dados no qual o esquema de partição foi criado.  
  
-   Permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual o esquema de partição foi criado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para modificar um esquema de partição:**  
  
 Essa ação específica não pode ser executada com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para modificar um esquema de partição, primeiro você deve excluir o esquema e depois criar um novo com as propriedades desejadas usando o Assistente para Criar Partição. Para obter mais informações, consulte [Create Partitioned Tables and Indexes](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)[Using SQL Server Management Studio](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md#SSMSProcedure) em **Criar tabelas e índices particionados**.  
  
#### <a name="to-delete-a-partition-scheme"></a>Para excluir um esquema de partição  
  
1.  Clique no sinal de adição para expandir o banco de dados onde você quer excluir um esquema de partição.  
  
2.  Clique no sinal de adição para expandir a pasta **Armazenamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Esquemas de Partição** .  
  
4.  Clique com o botão direito do mouse no esquema de partição a ser excluído e selecione **Excluir**.  
  
5.  Na caixa de diálogo **Excluir Objeto** , verifique se o esquema de partição correto está selecionado e clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-modify-a-partition-scheme"></a>Para modificar um esquema de partição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- add five new filegroups to the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test1fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test4fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test5fg;  
    GO  
    -- if the "myRangePF1" partition function and the "myRangePS1" partition scheme exist,  
    -- drop them from the AdventureWorks2012 database  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
    DROP PARTITION FUNCTION myRangePF1;  
    GO  
    IF EXISTS (SELECT * FROM sys.partition_schemes  
        WHERE name = 'myRangePS1')  
    DROP PARTITION SCHEME myRangePS1;  
    GO  
    -- create the new partition function "myRangePF1" with four partition groups  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    -- create the new partition scheme "myRangePS1"that will use   
    -- the "myRangePF1" partition function with five file groups.  
    -- The last filegroup, "test5fg," will be kept empty but marked  
    -- as the next used filegroup in the partition scheme.  
    CREATE PARTITION SCHEME myRangePS1  
    AS PARTITION myRangePF1  
    TO (test1fg, test2fg, test3fg, test4fg, test5fg);  
    GO  
    --Split "myRangePS1" between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    GO  
    -- Allow the "myRangePS1" partition scheme to use the filegroup "test5fg"  
    -- for the partition with boundary_values of 100 and 500  
    ALTER PARTITION SCHEME myRangePS1  
    NEXT USED test5fg;  
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md).  
  
  
