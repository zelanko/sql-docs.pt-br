---
title: Especificar mapeamentos de tipo de dados para um Publicador Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 99e1d3377cb5ed4afd4577462e0b436bb16d2fee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68941093"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Especificar mapeamentos de tipo de dados para um Publicador Oracle
  Este tópico descreve como especificar mapeamentos de tipo de dados para um Publicador Oracle no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Embora um conjunto de mapeamentos de tipo de dados padrão seja fornecidos para Publicadores Oracle, pode ser necessário especificar diferentes mapeamentos para determinada publicação.  
  
 **Neste tópico**  
  
-   **Para especificar mapeamentos de tipo de dados para um Publicador Oracle, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique mapeamentos de tipo de dados na guia **Mapeamento de Dados** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**. Isso está disponível na página **Artigos** do Assistente para Nova Publicação e na caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma Publicação de um Banco de Dados Oracle](create-a-publication-from-an-oracle-database.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-data-type-mapping"></a>Para especificar um mapeamento de tipo de dados  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione uma tabela e clique em **Propriedades do Artigo**.  
  
2.  Clique em **Definir as Propriedades do Artigo Realçado da Tabela**.  
  
3.  Na guia **Mapeamento de Dados** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**, selecione os mapeamentos da coluna **Tipo de Dados de Assinante**:  
  
    -   Para alguns tipos de dados, há somente um mapeamento possível; em tal caso, a coluna na grade de propriedades é somente leitura.  
  
    -   Para alguns tipos, é possível selecionar mais de uma opção. A[!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda que você use o mapeamento padrão, a menos que seu aplicativo exija um mapeamento diferente. Para obter mais informações, consulte [Mapeamento de tipo de dados para Publicadores Oracle ](../non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode especificar programaticamente mapeamentos de tipo de dados personalizados usando procedimentos armazenados de replicação. Você também pode definir os mapeamentos padrão que são usados ao mapear tipos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dados entre o e[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] um DBMS (sistema de gerenciamento de não-banco de dados). Para obter mais informações, consulte [Mapeamento de tipo de dados para Publicadores Oracle ](../non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Para definir mapeamentos de tipo de dados personalizados ao criar um artigo que pertence a uma publicação Oracle  
  
1.  Se já não houver uma, crie uma publicação Oracle.  
  
2.  No Distribuidor, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique um valor **0** para **\@use_default_datatypes**. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
3.  No Distribuidor, execute [sp_helparticlecolumns](/sql/relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql) para exibir o mapeamento existente para uma coluna em um artigo publicado.  
  
4.  No Distribuidor, execute [sp_changearticlecolumndatatype](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql). Especifique o nome do editor Oracle para ** \@o Publicador**, bem como a ** \@publicação**, ** \@o artigo**e ** \@a coluna** para definir a coluna publicada. Especifique o nome do tipo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de dados a ser mapeado para o ** \@tipo**, bem como ** \@comprimento**, ** \@precisão**e ** \@escala**, quando aplicável.  
  
5.  No Distribuidor, execute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Isso cria a exibição usada para gerar o instantâneo da publicação Oracle.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>Para especificar um mapeamento como mapeamento padrão para um tipo de dados  
  
1.  (Opcional) No Distribuidor de qualquer banco de dados, execute [sp_getdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql). Especifique ** \@source_dbms**, ** \@source_type**, ** \@destination_dbms**, ** \@destination_version**e quaisquer outros parâmetros necessários para identificar o DBMS de origem. As informações sobre o tipo de dados atualmente mapeados no DBMS de destino são retornadas usando os parâmetros de saída.  
  
2.  (Opcional) Para o Distribuidor em qualquer banco de dados, execute [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql). Especifique ** \@source_dbms** e quaisquer outros parâmetros necessários para filtrar o conjunto de resultados. Observe o valor de **mapping_id** para o mapeamento desejado no conjunto de resultados.  
  
3.  (Opcional) No Distribuidor em qualquer banco de dados, execute [sp_getdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql).  
  
    -   Se você souber o valor desejado de **mapping_id** obtido na etapa 2, especifique-o para **\@mapping_id**.  
  
    -   Se não souber o **mapping_id**, especifique os parâmetros **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_type** e quaisquer outros parâmetros necessários para identificar um mapeamento existente.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>Para localizar tipos de dados válidos para um determinado tipo de dados Oracle  
  
1.  No Distribuidor em qualquer banco de dados, execute [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql). Especifique um valor de **Oracle** para ** \@source_dbms** e quaisquer outros parâmetros necessários para filtrar o conjunto de resultados.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a>Exemplos (Transact-SQL)  
 Este exemplo altera uma coluna com um tipo de dados Oracle de NUMBER, de modo que ele seja mapeado para o tipo de dados `numeric`(38,38) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], em vez do tipo de dados padrão `float`.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_changecolumndatatype)]  
  
 Este exemplo de consulta retorna os mapeamentos padrão e alternativos para o tipo de dados `CHAR` do Oracle 9.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_char)]  
  
 Este exemplo de consulta retorna os mapeamentos padrão para o tipo de dados `NUMBER` do Oracle 9 quando ele é especificado sem uma escala ou precisão.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_number)]  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeamento de tipo de dados para Publicadores Oracle](../non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Replicação de banco de dados heterogêneo](../non-sql/heterogeneous-database-replication.md)   
 [Conceitos de procedimentos armazenados do sistema de replicação](../concepts/replication-system-stored-procedures-concepts.md)   
 [Configurar um Publicador Oracle](../non-sql/configure-an-oracle-publisher.md)  
  
  
