---
description: Criar índices com colunas incluídas
title: Criar índices com colunas incluídas | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index size [SQL Server]
- index keys [SQL Server]
- index columns [SQL Server]
- size [SQL Server], indexes
- key columns [SQL Server]
- included columns
- nonclustered indexes [SQL Server], included columns
- designing indexes [SQL Server], included columns
- nonkey columns
ms.assetid: d198648d-fea5-416d-9f30-f9d4aebbf4ec
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4b7c552fa3955818c8d9978802f950f07f8a6bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88408262"
---
# <a name="create-indexes-with-included-columns"></a>Criar índices com colunas incluídas
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este tópico descreve como adicionar colunas incluído (ou não chave) para estender a funcionalidade de índices não clusterizados no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ao incluir colunas não chave, você pode criar você índices não clusterizados que abrangem mais consultas. Isto porque as colunas não chave têm os seguintes benefícios:  
  
-   Elas podem ser tipos de dados não permitidos como colunas de chave de índice.  
-   Eles não são considerados pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao calcular o número de colunas de chave de índice ou o tamanho da chave de índice.  
  
 Um índice com colunas não chave pode melhorar o desempenho de consulta significativamente quando todas as colunas na consulta são incluídas no índice como colunas de chave ou não chave. Os ganhos de desempenho são alcançados pois o otimizador de consulta pode localizar todos os valores de coluna dentro do índice, a tabela, ou dados de índice clusterizado não são acessados, resultando em poucas operações de E/S de disco.  
  
> [!NOTE]  
> Quando um índice contém todas as colunas referenciadas por uma consulta, ele costuma ser referenciado como se *abrangendo a consulta*.  
   
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="design-recommendations"></a><a name="DesignRecs"></a> Recomendações de design  
  
-   Redesenhe índices não clusterizados que tenham um tamanho grande de chave de índice, de tal forma que apenas as colunas usadas para buscas e pesquisas sejam colunas de chave. Transforme todas as outras colunas que abrangem a consulta em colunas não chave. Deste modo, você terá todas as colunas necessárias para abranger a consulta, mas a chave de índice em si é pequena e eficiente.  
  
-   Inclua colunas não chave em um índice não clusterizado para evitar exceder as limitações do tamanho atual do índice de um máximo de 32 colunas de chave e um tamanho máximo de chave de índice de 1.700 bytes (16 colunas de chave e 900 bytes antes de [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]). O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não considera as colunas não chave ao calcular o número de colunas de chave de índice, ou o tamanho da chave do índice.  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   As colunas não chave só podem ser definidas em índices não clusterizados.  
  
-   Todos os tipos de dados, exceto **text**, **ntext**e **image** , podem ser usados como colunas não chave.  
  
-   As colunas computadas que são determinísticas e precisas ou imprecisas podem ser colunas não chave. Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
-   As colunas computadas derivadas dos tipos de dados **image**, **ntext**e **text** podem ser colunas não chave, desde que o tipo de dados da coluna computada seja permitido como uma coluna de índice não chave.  
  
-   As colunas que não são de chave não podem ser removidas de uma tabela, a menos que o índice dessa tabela seja removido primeiro.  
  
-   As colunas não chave não podem ser alteradas, exceto para fazerem o seguinte:  
  
    -   Alterar a nulidade da coluna da coluna NOT NULL até NULL.  
  
    -   Aumente o tamanho das colunas **varchar**, **nvarchar**ou **varbinary** .  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>Para criar um índice com colunas não chave  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja criar um índice com colunas não chave.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja criar um índice com colunas não chave.  
  
4.  Clique com o botão direito do mouse na pasta **Índices**, aponte para **Novo Índice** e selecione **Índice Não Clusterizado...** .  
  
5.  Na caixa de diálogo **Novo Índice** , na página **Geral** , insira o nome do novo índice na caixa **Nome do índice** .  
  
6.  Na guia **Colunas de chave de índice**, clique em **Adicionar...** .  
  
7.  Na caixa de diálogo **Selecionar colunas de** _table\_name_, marque as caixas de seleção das colunas da tabela a serem adicionadas ao índice.  
  
8.  Clique em **OK**.  
  
9. Na guia **Colunas incluídas**, clique em **Adicionar...** .  
  
10. Na caixa de diálogo **Selecionar colunas de**_table\_name_, marque as caixas de seleção das colunas da tabela ou as colunas a serem adicionadas ao índice como colunas não chave.  
  
11. Clique em **OK**.  
  
12. Na caixa de diálogo **Novo Índice** , clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>Para criar um índice com colunas não chave  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Creates a nonclustered index on the Person.Address table with four included (nonkey) columns.   
    -- index key column is PostalCode and the nonkey columns are  
    -- AddressLine1, AddressLine2, City, and StateProvinceID.  
    CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
    GO  
    ```  

## <a name="related-content"></a>Conteúdo relacionado  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
[Guia de criação de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md)   
