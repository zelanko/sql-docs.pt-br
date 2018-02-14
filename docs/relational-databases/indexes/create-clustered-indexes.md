---
title: "Criar índices clusterizados | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index creation [SQL Server], clustered indexes
- clustered indexes, creating
- clustered indexes, PRIMARY KEY constraint
- clustered indexes, UNIQUE constraint
- indexes [SQL Server], clustered
ms.assetid: 47148383-c2c7-4f08-a9e4-7016bf2d1d13
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: f7aa0ca2f5ea1ffe7ec54cc6279fbf5f1218f8c0
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="create-clustered-indexes"></a>Criar índices clusterizados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  É possível criar índices clusterizados em tabelas usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Com poucas exceções, toda tabela deveria ter um índice clusterizado. Além de melhorar o desempenho da consulta, o índice clusterizado pode ser recompilado ou reorganizado sob demanda para controlar a fragmentação de tabela. Um índice clusterizado também pode ser criado em uma exibição. (Os índices clusterizados são definidos no tópico [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md).)  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Implementações comuns](#Implementations)  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um índice clusterizado em uma tabela, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Implementations"></a> Implementações comuns  
 Os índices clusterizados são implementados das seguintes maneiras:  
  
-   **Restrições PRIMARY KEY e UNIQUE**  
  
     Quando se cria uma restrição PRIMARY KEY, é criado automaticamente um índice clusterizado exclusivo na coluna ou a coluna é automaticamente criada se não existir um índice clusterizado na tabela e você não especificar um índice não clusterizado exclusivo. A coluna de chave primária não pode permitir valores NULL.  
  
     Quando se cria uma restrição UNIQUE, é criado, por padrão, um índice não clusterizado exclusivo para impor uma restrição UNIQUE por padrão. Você pode especificar um índice clusterizado exclusivo caso ainda não exista um índice clusterizado na tabela.  
  
     O índice criado como parte da restrição recebe automaticamente o mesmo nome da restrição. Para obter mais informações, consulte [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md) e [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
-   **Índice independente de uma restrição**  
  
     Você pode criar um índice clusterizado em uma coluna diferente da coluna de chave primária se uma restrição de chave primária não clusterizada tiver sido especificada.  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Quando uma estrutura de índice clusterizado é criada, o espaço em disco de ambas as estruturas, a antiga (origem) e a nova (destino), é necessário em seus respectivos arquivos e grupos de arquivos. A antiga estrutura não é desalocada até que a transação completa seja confirmada. Pode igualmente ser necessário espaço temporário em disco adicional, para classificação. Para obter mais informações, consulte [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
-   Se um índice clusterizado for criado em uma pilha com vários índices não clusterizados existentes, todos os índices não clusterizados deverão ser recriados de modo que contenham o valor de chave de clusterização em vez do RID (Identificador de Linha). Da mesma forma, se um índice clusterizado for cancelado em uma tabela com vários índices não clusterizados, os índices não clusterizados serão todos recriados como parte da operação DROP. Isso pode despender um tempo significativo em tabelas grandes.  
  
     A forma preferencial de criação de índices em tabelas grandes é iniciar com o índice clusterizado e depois criar os índices não clusterizados. Considere a definição da opção ONLINE como ON ao criar índices em tabelas existentes. Quando definidos como ON, os bloqueios de tabela não são mantidos a longo prazo. Isso permite consultas ou atualizações à tabela subjacente para continuar. Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
-   A chave de um índice clusterizado não pode conter colunas **varchar** que tenham dados existentes na unidade de alocação ROW_OVERFLOW_DATA. Se um índice clusterizado for criado em uma coluna **varchar** e os dados existentes estiverem na unidade de alocação IN_ROW_DATA, as ações subsequentes de inserção ou atualização na coluna que faria o push dos dados da linha apresentarão falha. Para obter informações sobre tabelas que podem conter dados de estouro de linha, use a função de gerenciamento dinâmico [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>Para criar um índice clusterizado usando o Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, expanda a tabela na qual você deseja criar um índice clusterizado.  
  
2.  Clique com o botão direito do mouse na pasta **Índices** , aponte para **Novo Índice**e selecione **Índice Clusterizado…**.  
  
3.  Na caixa de diálogo **Novo Índice** , na página **Geral** , insira o nome do novo índice na caixa **Nome do índice** .  
  
4.  Na guia **Colunas de chave de índice**, clique em **Adicionar…**.  
  
5.  Na caixa de diálogo **Selecionar Colunas de***table_name*, marque a caixa de seleção da coluna de tabela a ser adicionada ao índice clusterizado.  
  
6.  Clique em **OK**.  
  
7.  Na caixa de diálogo **Novo Índice** , clique em **OK**.  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>Para criar um índice clusterizado usando o Designer de Tabela  
  
1.  No Pesquisador de Objetos, expanda o banco de dados na qual você deseja criar uma tabela com um índice clusterizado.  
  
2.  Clique com o botão direito do mouse na pasta **Tabelas** e clique em **Nova Tabela...**.  
  
3.  Crie uma tabela como você faria normalmente. Para obter mais informações, veja [Criar tabelas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/create-tables-database-engine.md).  
  
4.  Clique com o botão direito do mouse na tabela criada acima e selecione **Design**.  
  
5.  No menu **Designer de Tabela** , clique em **Índices/Chaves**.  
  
6.  Na caixa de diálogo **Índices/Chaves** , clique em **Adicionar**.  
  
7.  Selecione o novo índice na caixa de texto **Índice ou Chave Exclusiva/Primária Selecionada** .  
  
8.  Na grade, selecione **Criar como Clusterizado**e selecione **Sim** na lista suspensa, à direita da propriedade.  
  
9. Clique em **Fechar**.  
  
10. No menu **Arquivo**, clique em **Salvar***table_name*.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-clustered-index"></a>Para criar um índice clusterizado  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO  
    ```  
  
 Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar chaves primárias](../../relational-databases/tables/create-primary-keys.md)   
 [Criar restrições exclusivas](../../relational-databases/tables/create-unique-constraints.md)  
  
  
