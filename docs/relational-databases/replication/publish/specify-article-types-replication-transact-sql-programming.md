---
title: "Especificar tipos de artigo (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "publicação [replicação do SQL Server], execução de procedimento armazenado"
  - "artigos [replicação do SQL Server], opções de replicação transacional"
  - "artigos [replicação do SQL Server], opções de replicação de mesclagem"
  - "procedimentos armazenados [replicação do SQL Server], publicação"
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Especificar tipos de artigo (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Os tipos de artigo padrão para replicação são artigos da tabela, mas é possível publicar outros objetos de banco de dados como artigos, inclusive exibições, procedimentos armazenados, funções definidas pelo usuário e execução de procedimento armazenado. Você pode usar procedimentos armazenados de replicação para especificar um tipo de artigo programaticamente quando definir um artigo. Os procedimentos usados dependerão do tipo de replicação e do tipo de artigo.  
  
> [!NOTE]  
>  A designação somente esquema, ao definir tabela, exibição e artigos de procedimento armazenado, indica que apenas a definição de objeto é replicada.  
  
### Para publicar um artigo de tabela em uma publicação transacional ou de instantâneo  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique um dos valores a seguir para **@type** para definir o tipo de artigo:  
  
    -   **logbased** -um artigo de tabela com base em log, que é o padrão para replicação transacional e de instantâneo. A replicação gera automaticamente o procedimento armazenado usado para filtragem horizontal e a exibição que define um artigo filtrado verticalmente.  
  
    -   **logbased manualfilter** -um artigo filtrado horizontalmente, baseado em log, em que o procedimento armazenado usado para filtragem horizontal é manualmente criado e definido pelo usuário e especificado para **@filter**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **logbased manualview** -um artigo filtrado verticalmente, com base em log, onde o modo de exibição que define o artigo filtrado verticalmente é criado e definido pelo usuário e especificado para **@sync_object**. Para obter mais informações, consulte [definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [definir e modificar um filtro de coluna](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **logbased manualboth** -um baseado em log, horizontalmente e verticalmente filtrados artigo onde tanto o procedimento armazenado usado para filtragem horizontal e o modo de exibição que define o artigo filtrado verticalmente são criados e definidos pelo usuário e especificado para **@filter** e **@sync_object**, respectivamente. Para obter mais informações, consulte [definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [definir e modificar um filtro de coluna](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Para **logbased manualboth** e **logbased manualfilter** artigos, execute [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) para gerar o procedimento armazenado de filtragem para um artigo filtrado horizontalmente. Para obter mais informações, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para **logbased manualboth**, **logbased manualview**, e **logbased manualfilter** artigos, execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) para gerar o modo de exibição que define o artigo filtrado verticalmente. Para obter mais informações, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### Para publicar uma exibição ou artigo de exibição indexada em uma publicação transacional ou de instantâneo  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique um dos valores a seguir para **@type** para definir o tipo de artigo:  
  
    -   **indexado view logbased** -um artigo de modo de exibição indexado baseado em log. A replicação gera automaticamente o procedimento armazenado usado para filtragem horizontal e a exibição que define um artigo filtrado verticalmente.  
  
    -   **Exibir o esquema somente** -um artigo de exibição somente de esquema. A tabela base também deve ser replicada.  
  
    -   **somente esquema de modo de exibição indexado** -um artigo somente de esquema de exibição indexada. A tabela base também deve ser replicada.  
  
    -   **indexado view logbased manualfilter** -um artigo filtrado horizontalmente, baseado em log, exibição indexada em que o procedimento armazenado usado para filtragem horizontal é manualmente criado e definido pelo usuário e especificado para **@filter**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **indexado view logbased manualview** -um artigo de exibição indexada filtrado, baseado em log, em que o modo de exibição que define um artigo filtrado verticalmente é criado e definido pelo usuário e especificado para **@sync_object**. Para obter mais informações, consulte [definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [definir e modificar um filtro de coluna](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **indexado view logbased manualboth** -um artigo de exibição indexada filtrado, baseado em log, onde tanto o procedimento armazenado usado para filtragem horizontal e o modo de exibição que define um artigo filtrado verticalmente são criados e definidos pelo usuário e especificado para **@filter** e **@sync_object**, respectivamente. Para obter mais informações, consulte [definir e modificar um filtro de linha estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [definir e modificar um filtro de coluna](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Para **logbased manualboth** e **logbased manualfilter** artigos, execute [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) para gerar o procedimento armazenado de filtragem para um artigo filtrado horizontalmente. Para obter mais informações, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Para **logbased manualboth**, **logbased manualview**, e **logbased manualfilter** artigos, execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) para gerar o modo de exibição que define o artigo filtrado verticalmente. Para obter mais informações, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### Para publicar um procedimento armazenado, execução de procedimento armazenado ou artigo de função definida pelo usuário em uma publicação transacional ou de instantâneo  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique um dos valores a seguir para **@type** para definir o tipo de artigo:  
  
    -   **somente esquema de PROC** -um artigo somente de esquema de procedimento armazenado.  
  
    -   **proc exec** -replica a execução do procedimento armazenado para todos os assinantes do artigo. Para obter mais informações, consulte [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **Serializable proc exec** -replica a execução do procedimento armazenado apenas se ele for executado no contexto de uma transação serializável. Para obter mais informações, consulte [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **somente esquema de função** -um artigo somente de esquema de função definida pelo usuário.  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### Para publicar um artigo de tabela ou de exibição em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique um dos valores a seguir para **@type** para definir o tipo de artigo:  
  
    -   **tabela** -um artigo de tabela.  
  
    -   **somente esquema de modo de exibição indexado** -um artigo somente de esquema de exibição indexada.  
  
    -   **Exibir o esquema somente** -um artigo de exibição somente de esquema.  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
### Para publicar um procedimento armazenado ou artigo de função definida pelo usuário em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique um dos valores a seguir para **@type** para definir o tipo de artigo:  
  
    -   **somente esquema de função** -um artigo somente de esquema de função definida pelo usuário.  
  
    -   **somente esquema de PROC** -um artigo somente de esquema de procedimento armazenado.  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Consulte também  
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  