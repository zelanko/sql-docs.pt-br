---
title: Especificar tipos de artigo (Programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0a88b719e45881bf8abed1b6b9331cd9d2d4502e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120551"
---
# <a name="specify-article-types-replication-transact-sql-programming"></a>Especificar tipos de artigo (Programação Transact-SQL de replicação)
  Os tipos de artigo padrão para replicação são artigos da tabela, mas é possível publicar outros objetos de banco de dados como artigos, inclusive exibições, procedimentos armazenados, funções definidas pelo usuário e execução de procedimento armazenado. Você pode usar procedimentos armazenados de replicação para especificar um tipo de artigo programaticamente quando definir um artigo. Os procedimentos usados dependerão do tipo de replicação e do tipo de artigo.  
  
> [!NOTE]  
>  A designação somente esquema, ao definir tabela, exibição e artigos de procedimento armazenado, indica que apenas a definição de objeto é replicada.  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>Para publicar um artigo de tabela em uma publicação transacional ou de instantâneo  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique um dos seguintes valores para **@type** para definir o tipo de artigo:  
  
    -   **logbased** - um artigo de tabela baseado em log que é o padrão para replicação transacional e de instantâneo. A replicação gera automaticamente o procedimento armazenado usado para filtragem horizontal e a exibição que define um artigo filtrado verticalmente.  
  
    -   **logbased manualfilter** - um artigo filtrado horizontalmente, baseado em log, em que o procedimento armazenado usado para filtragem horizontal é criado manualmente, definido pelo usuário e especificado para **@filter**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
    -   **logbased manualview** - um artigo filtrado verticalmente, baseado em log, em que a exibição que define o artigo filtrado verticalmente é criada e definida pelo usuário e especificada para **@sync_object**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
    -   **logbased manualboth** - um artigo filtrado horizontal e verticalmente, baseado em log, em que tanto o procedimento armazenado usado para filtragem horizontal quanto a exibição que define o artigo filtrado verticalmente são criados e definidos pelo usuário e especificados respectivamente para **@filter** e **@sync_object**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
2.  Para artigos **logbased manualboth** e **logbased manualfilter** , execute [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) para gerar o procedimento armazenado de filtragem para um artigo filtrado horizontalmente. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
3.  Para artigos **logbased manualboth**, **logbased manualview**e **logbased manualfilter** , execute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) para gerar a exibição que define o artigo filtrado verticalmente. Para obter mais informações, consulte [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>Para publicar uma exibição ou artigo de exibição indexada em uma publicação transacional ou de instantâneo  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique um dos seguintes valores para **@type** para definir o tipo de artigo:  
  
    -   **indexed view logbased** - um artigo de exibição indexada baseado em log. A replicação gera automaticamente o procedimento armazenado usado para filtragem horizontal e a exibição que define um artigo filtrado verticalmente.  
  
    -   **view schema only** - um artigo de exibição somente de esquema. A tabela base também deve ser replicada.  
  
    -   **indexed view schema only** - um artigo de exibição indexada somente de esquema. A tabela base também deve ser replicada.  
  
    -   **indexed view logbased manualfilter** - um artigo de exibição indexada, filtrado horizontalmente, baseado em log, em que o procedimento armazenado usado para filtragem horizontal é criado manualmente, definido pelo usuário e especificado para **@filter**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
    -   **indexed view logbased manualview** - um artigo de exibição indexada, filtrado, baseado em log, em que a exibição que define um artigo filtrado verticalmente é criada e definida pelo usuário e especificada para **@sync_object**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
    -   **indexed view logbased manualboth** - um artigo de exibição indexada, filtrado, baseado em log, em que tanto o procedimento armazenado usado para filtragem horizontal quanto a exibição que define um artigo filtrado verticalmente são criados e definidos pelo usuário e especificados respectivamente para **@filter** e **@sync_object**. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
2.  Para artigos **logbased manualboth** e **logbased manualfilter** , execute [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) para gerar o procedimento armazenado de filtragem para um artigo filtrado horizontalmente. Para obter mais informações, consulte [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
3.  Para artigos **logbased manualboth**, **logbased manualview**e **logbased manualfilter** , execute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) para gerar a exibição que define o artigo filtrado verticalmente. Para obter mais informações, consulte [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>Para publicar um procedimento armazenado, execução de procedimento armazenado ou artigo de função definida pelo usuário em uma publicação transacional ou de instantâneo  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique um dos seguintes valores para **@type** para definir o tipo de artigo:  
  
    -   **proc schema only** - um artigo de procedimento armazenado de somente esquema.  
  
    -   **proc exec** - replica a execução do procedimento armazenado para todos os Assinantes do artigo. Para saber mais, confira [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **serializable proc exec** - replica a execução do procedimento armazenado apenas se for executado no contexto de uma transação serializável. Para saber mais, confira [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **func schema only** - um artigo de função definida pelo usuário e somente de esquema.  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>Para publicar um artigo de tabela ou de exibição em uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique um dos seguintes valores para **@type** para definir o tipo de artigo:  
  
    -   **table** - um artigo de tabela.  
  
    -   **indexed view schema only** - um artigo de exibição indexada somente de esquema.  
  
    -   **view schema only** - um artigo de exibição somente de esquema.  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>Para publicar um procedimento armazenado ou artigo de função definida pelo usuário em uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique um dos seguintes valores para **@type** para definir o tipo de artigo:  
  
    -   **func schema only** - um artigo de função definida pelo usuário e somente de esquema.  
  
    -   **proc schema only** - um artigo de procedimento armazenado de somente esquema.  
  
     Isso define um novo artigo para a publicação. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
## <a name="see-also"></a>Consulte também  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md)  
  
  
