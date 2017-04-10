---
title: "Especificar mapeamentos de tipo de dados para um Publicador Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicação Oracle [replicação do SQL Server], mapeamento de tipos de dados"
  - "publicação Oracle [replicação do SQL Server], publicação Oracle"
  - "mapeando tipos de dados [replicação do SQL Server]"
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Especificar mapeamentos de tipo de dados para um Publicador Oracle
  Este tópico descreve como especificar mapeamentos de tipo de dados para um Publicador Oracle no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Embora um conjunto de mapeamentos de tipo de dados padrão seja fornecidos para Publicadores Oracle, pode ser necessário especificar diferentes mapeamentos para determinada publicação.  
  
 **Neste tópico**  
  
-   **Para especificar mapeamentos de tipo de dados para um Publicador Oracle, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especificar mapeamentos de tipo de dados no **mapeamento de dados** guia o **Propriedades do artigo - \< artigo>** caixa de diálogo. Está disponível no **artigos** página do Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação de um banco de dados Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar um mapeamento de tipo de dados  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela e, em seguida, clique em **Propriedades do artigo**.  
  
2.  Clique em **Definir as Propriedades do Artigo Realçado da Tabela**.  
  
3.  No **mapeamento de dados** Guia do **Propriedades do artigo - \< artigo>** caixa de diálogo, selecione os mapeamentos do **tipo de dados do assinante** coluna:  
  
    -   Para alguns tipos de dados, há somente um mapeamento possível; em tal caso, a coluna na grade de propriedades é somente leitura.  
  
    -   Para alguns tipos, é possível selecionar mais de uma opção. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda que você use o mapeamento padrão, a menos que seu aplicativo exija um mapeamento diferente. Para obter mais informações, consulte [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Você pode especificar programaticamente mapeamentos de tipo de dados personalizados usando procedimentos armazenados de replicação. Você também pode definir os mapeamentos padrão que são usados quando os tipos de dados de mapeamento entre [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados (DBMS) do sistema de gerenciamento. Para obter mais informações, consulte [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### Para definir mapeamentos de tipo de dados personalizados ao criar um artigo que pertence a uma publicação Oracle  
  
1.  Se já não houver uma, crie uma publicação Oracle.  
  
2.  No distribuidor, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique um valor de **0** para **@use_default_datatypes**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  No distribuidor, execute [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) para exibir o mapeamento existente para uma coluna em um artigo publicado.  
  
4.  No distribuidor, execute [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md). Especifique o nome do Editor Oracle para **@publisher**, assim como para **@publication**, **@article**e **@column** , para definir a coluna publicada. Especifique o nome do tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a mapear para **@type**, assim como para **@length**, **@precision**e **@scale**, onde aplicável.  
  
5.  No distribuidor, execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Isso cria a exibição usada para gerar o instantâneo da publicação Oracle.  
  
#### Para especificar um mapeamento como mapeamento padrão para um tipo de dados  
  
1.  (Opcional) No distribuidor em qualquer banco de dados, execute [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md). Especifique **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_version**, e quaisquer outros parâmetros necessários para identificar o DBMS de origem. As informações sobre o tipo de dados atualmente mapeados no DBMS de destino são retornadas usando os parâmetros de saída.  
  
2.  (Opcional) No distribuidor em qualquer banco de dados, execute [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Especifique **@source_dbms** e quaisquer outros parâmetros necessários para filtrar o conjunto de resultados. Observe o valor de **mapping_id** para o mapeamento desejado no resultado definido.  
  
3.  No distribuidor em qualquer banco de dados, execute [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md).  
  
    -   Se você souber o valor desejado de **mapping_id** obtida na etapa 2, especifique-o para **@mapping_id**.  
  
    -   Se você não souber o **mapping_id**, especifique os parâmetros **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_type**, e quaisquer outros parâmetros necessários para identificar um mapeamento existente.  
  
#### Para localizar tipos de dados válidos para um determinado tipo de dados Oracle  
  
1.  No distribuidor em qualquer banco de dados, execute [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). Especifique um valor de **ORACLE** para **@source_dbms** e quaisquer outros parâmetros necessários para filtrar o conjunto de resultados.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este exemplo altera uma coluna com um tipo de dados Oracle do número de modo que ele é mapeado para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de dados **numéricos**(38,38), em vez do tipo de dados padrão **float**.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 Este exemplo de consulta retorna os mapeamentos padrão e mapeamentos alternativos para o tipo de dados **CHAR**do Oracle 9.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 Este exemplo de consulta retorna os mapeamentos padrão para o tipo de dados **NUMBER** do Oracle 9 quando ele é especificado sem uma escala ou precisão.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## Consulte também  
 [Mapeamento de tipo de dados para Publicadores Oracle ](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Replicação de banco de dados heterogênea](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar um publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  