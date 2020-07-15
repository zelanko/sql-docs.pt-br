---
title: Mapeamentos de tipo de dados para um Editor do Oracle
description: Descreve como especificar mapeamentos de tipo de dados para um Editor Oracle no SQL Server usando o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a58c4a27a90a36acc47c3338b39a802a2209060d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900649"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Especificar mapeamentos de tipo de dados para um Publicador Oracle
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como especificar mapeamentos de tipo de dados para um Publicador Oracle no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Embora um conjunto de mapeamentos de tipo de dados padrão seja fornecidos para Publicadores Oracle, pode ser necessário especificar diferentes mapeamentos para determinada publicação.  
  
 **Neste tópico**  
  
-   **Para especificar mapeamentos de tipo de dados para um Publicador Oracle, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique mapeamentos de tipo de dados na guia **Mapeamento de Dados** da caixa de diálogo **Propriedades do Artigo – \<Article>** . Isso está disponível na página **Artigos** do Assistente para Nova Publicação e na caixa de diálogo **Propriedades de Publicação – \<Publication>** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma Publicação de um Banco de Dados Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-data-type-mapping"></a>Para especificar um mapeamento de tipo de dados  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publication>** , selecione uma tabela e clique em **Propriedades do Artigo**.  
  
2.  Clique em **Definir as Propriedades do Artigo Realçado da Tabela**.  
  
3.  Na guia **Mapeamento de Dados** da caixa de diálogo **Propriedades do Artigo – \<Article>** , selecione os mapeamentos na coluna **Tipo de Dados do Assinante**:  
  
    -   Para alguns tipos de dados, há somente um mapeamento possível; em tal caso, a coluna na grade de propriedades é somente leitura.  
  
    -   Para alguns tipos, é possível selecionar mais de uma opção. A[!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda que você use o mapeamento padrão, a menos que seu aplicativo exija um mapeamento diferente. Para obter mais informações, consulte [Mapeamento de tipo de dados para Publicadores Oracle ](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode especificar programaticamente mapeamentos de tipo de dados personalizados usando procedimentos armazenados de replicação. Você pode também definir os mapeamentos padrão que são usados ao mapear tipos de dados entre o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um DBMS (sistema de gerenciamento de banco de dados) que não seja do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Mapeamento de tipo de dados para Publicadores Oracle ](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Para definir mapeamentos de tipo de dados personalizados ao criar um artigo que pertence a uma publicação Oracle  
  
1.  Se já não houver uma, crie uma publicação Oracle.  
  
2.  No Distribuidor, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique um valor **0** para **\@use_default_datatypes**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  No Distribuidor, execute [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) para exibir o mapeamento existente para uma coluna em um artigo publicado.  
  
4.  No Distribuidor, execute [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md). Especifique o nome do Editor Oracle para **\@publisher**, assim como para **\@publication**, **\@article** e **\@column**, para definir a coluna publicada. Especifique o nome do tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a mapear para **\@type**, assim como para **\@length**, **\@precision** e **\@scale**, onde aplicável.  
  
5.  No Distribuidor, execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Isso cria a exibição usada para gerar o instantâneo da publicação Oracle.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>Para especificar um mapeamento como mapeamento padrão para um tipo de dados  
  
1.  (Opcional) No Distribuidor de qualquer banco de dados, execute [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md). Especifique **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_version** e quaisquer outros parâmetros necessários para identificar a DBMS de origem. As informações sobre o tipo de dados atualmente mapeados no DBMS de destino são retornadas usando os parâmetros de saída.  
  
2.  (Opcional) Para o Distribuidor em qualquer banco de dados, execute [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Especifique **\@source_dbms** e quaisquer outros parâmetros necessários para filtrar o conjunto de resultados. Observe o valor de **mapping_id** para o mapeamento desejado no conjunto de resultados.  
  
3.  (Opcional) No Distribuidor em qualquer banco de dados, execute [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md).  
  
    -   Se você souber o valor desejado de **mapping_id** obtido na etapa 2, especifique-o para **\@mapping_id**.  
  
    -   Se não souber o **mapping_id**, especifique os parâmetros **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_type** e quaisquer outros parâmetros necessários para identificar um mapeamento existente.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>Para localizar tipos de dados válidos para um determinado tipo de dados Oracle  
  
1.  No Distribuidor em qualquer banco de dados, execute [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Especifique um valor de **ORACLE** para **\@source_dbms** e quaisquer outros parâmetros necessários para filtrar o conjunto de resultados.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este exemplo altera uma coluna com um tipo de dados Oracle de NUMBER, de modo que ele seja mapeado para o tipo de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (38,38) do **ssNoVersion**, em vez do tipo de dados padrão **float**.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 Este exemplo de consulta retorna os mapeamentos padrão e alternativos para o tipo de dados **CHAR**do Oracle 9.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 Este exemplo de consulta retorna os mapeamentos padrão para o tipo de dados **NUMBER** do Oracle 9 quando ele é especificado sem uma escala ou precisão.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Replicação de banco de dados heterogênea](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  
