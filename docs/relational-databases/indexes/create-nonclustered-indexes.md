---
description: Criar índices não clusterizados
title: Criar índices não clusterizados | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], nonclustered indexes
- nonclustered indexes [SQL Server], creating
- nonclustered indexes [SQL Server], UNIQUE constraint
- indexes [SQL Server], nonclustered
- nonclustered indexes [SQL Server], PRIMARY KEY constraint
ms.assetid: 9402029a-1227-46c4-93aa-c2122eb1b943
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04c45acc426cdeb187fd673756da388f971fe24e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88382612"
---
# <a name="create-nonclustered-indexes"></a>Criar índices não clusterizados
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Você pode criar índices não clusterizados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um índice não clusterizado é uma estrutura de índice separada dos dados armazenados em uma tabela que reorganiza um ou mais colunas selecionadas. Índices não clusterizados costumam ser uma forma mais rápida de localizar dados do que a busca na tabela subjacente; as consultas às vezes podem ser totalmente respondidas pelos dados no índice não clusterizado, ou o índice não clusterizado pode apontar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para as linhas na tabela subjacente. Geralmente, os índices não clusterizados são criados para aprimorar o desempenho de consultas utilizadas com frequência, não cobertas pelo índice clusterizado, ou para localizar linhas em uma tabela sem um índice clusterizado (denominado heap). Você pode criar vários índices não clusterizados em uma tabela ou exibição indexada.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="typical-implementations"></a><a name="Implementations"></a> Implementações comuns  
 Os índices não clusterizados são implementados das seguintes maneiras:  
  
-   **Restrições UNIQUE**  
  
     Quando se cria uma restrição UNIQUE, é criado, por padrão, um índice não clusterizado exclusivo para impor uma restrição UNIQUE por padrão. Você pode especificar um índice clusterizado exclusivo caso ainda não exista um índice clusterizado na tabela. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
-   **Índice independente de uma restrição**  
  
     Por padrão, será criado um índice não clusterizado se não for especificado como clusterizado. O número máximo de índices não clusterizados que podem ser criados em uma tabela é 999. Isso inclui qualquer índice criado por restrições PRIMARY KEY ou UNIQUE, mas não inclui índices XML.  
  
-   **Índice não clusterizado em uma exibição indexada**  
  
     Depois que for criado um índice clusterizado exclusivo em uma exibição, poderão ser criados índices não clusterizados. Para obter mais informações, veja [Criar exibições indexadas](../../relational-databases/views/create-indexed-views.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-nonclustered-index-by-using-the-table-designer"></a>Para criar um índice não clusterizado usando o Designer de Tabela  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja criar um índice não clusterizado.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Clique com o botão direito do mouse na tabela na qual você deseja criar um índice não clusterizado e selecione **Design**.  
  
4.  No menu **Designer de Tabela** , clique em **Índices/Chaves**.  
  
5.  Na caixa de diálogo **Índices/Chaves** , clique em **Adicionar**.  
  
6.  Selecione o novo índice na caixa de texto **Índice ou Chave Exclusiva/Primária Selecionada** .  
  
7.  Na grade, selecione **Criar como Clusterizado**e escolha **Não** na lista suspensa, à direita da propriedade.  
  
8.  Clique em **fechar**  
  
9. No menu **Arquivo** , clique em **Salvar**_table_name_.  

#### <a name="to-create-a-nonclustered-index-by-using-object-explorer"></a>Para criar um índice não clusterizado usando o Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja criar um índice não clusterizado.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Expanda a tabela na qual você deseja criar um índice não clusterizado.  
  
4.  Clique com o botão direito do mouse na pasta **Índices**, aponte para **Novo Índice** e selecione **Índice Não Clusterizado...** .  
  
5.  Na caixa de diálogo **Novo Índice** , na página **Geral** , insira o nome do novo índice na caixa **Nome do índice** .  
  
6.  Em **Colunas de chave de índice**, clique em **Adicionar...** .  
  
7.  Na caixa de diálogo **Selecionar Colunas de**_table_name_ , marque as caixas de seleção das colunas da tabela a serem adicionadas ao índice não clusterizado.  
  
8.  Clique em **OK**.  
  
9. Na caixa de diálogo **Novo Índice** , clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-nonclustered-index-on-a-table"></a>Para criar um índice não clusterizado em uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named IX_ProductVendor_VendorID and delete it if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
                WHERE name = N'IX_ProductVendor_VendorID')   
        DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;   
    GO  
    -- Create a nonclustered index called IX_ProductVendor_VendorID   
    -- on the Purchasing.ProductVendor table using the BusinessEntityID column.   
    CREATE NONCLUSTERED INDEX IX_ProductVendor_VendorID   
        ON Purchasing.ProductVendor (BusinessEntityID);   
    GO  
    ```  
  
## <a name="related-content"></a>Conteúdo relacionado  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
[Guia de criação de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md) 
