---
title: Excluir um artigo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
caps.latest.revision: "41"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57722c8edfeb9355a04377a225a5773cbed5dd5b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="delete-an-article"></a>Excluir um artigo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como excluir um artigo no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou RMO (Replication Management Objects). Para obter informações sobre as condições nas quais os artigos podem ser removidos e se a remoção de um artigo requer um novo instantâneo ou a reinicialização de assinaturas, consulte [Adicionar e remover artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **Neste tópico**  
  
-   **Para excluir um artigo, usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Os artigos podem ser excluídos de forma programática usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual o artigo pertence.  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>Para excluir um artigo de um instantâneo ou publicação transacional  
  
1.  Execute [sp_droparticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) para excluir um artigo, especificado por **@article**, de uma publicação, especificado por **@publication**. Especifique um valor de **1** para **@force_invalidate_snapshot**.  
  
2.  (Opcional) Para remover inteiramente o objeto publicado de um banco de dados, execute o comando `DROP <objectname>` no Publicador do banco de dados de publicação.  
  
#### <a name="to-delete-an-article-from-a-merge-publication"></a>Para excluir um artigo de uma publicação de mesclagem  
  
1.  Execute [sp_dropmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) para excluir um artigo, especificado por **@article**, de uma publicação, especificado por **@publication**. Se necessário, especifique um valor de **1** para **@force_invalidate_snapshot** e um valor de **1** para **@force_reinit_subscription**.  
  
2.  (Opcional) Para remover inteiramente o objeto publicado de um banco de dados, execute o comando `DROP <objectname>` no Publicador do banco de dados de publicação.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo a seguir exclui um artigo da publicação transacional. Como essa alteração invalida o instantâneo existente, um valor de **1** é especificado para o parâmetro **@force_invalidate_snapshot** .  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 O exemplo a seguir exclui dois artigos de uma publicação de mesclagem. Como essas alterações invalidam o instantâneo existente, um valor de **1** é especificado para o parâmetro **@force_invalidate_snapshot** .  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode excluir artigos programaticamente usando o RMO (Replication Management Objects). As classes RMO que você usa para excluir um artigo dependem do tipo de publicação a que o artigo pertence.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>Para excluir um artigo que pertence a uma publicação de instantâneo ou transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransArticle> .  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para se certificar de que o artigo existe. Se o valor desta propriedade for **false**, as propriedades do artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Feche todas as conexões.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>Para excluir um artigo que pertence a uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeArticle> .  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para se certificar de que o artigo existe. Se o valor desta propriedade for **false**, as propriedades do artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Feche todas as conexões.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar e remover artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
