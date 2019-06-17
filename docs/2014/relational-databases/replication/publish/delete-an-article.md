---
title: Excluir um artigo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce51b3fc6730b984c36aa44e87d3983233a3b006
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960864"
---
# <a name="delete-an-article"></a>Excluir um artigo
  Este tópico descreve como excluir um artigo no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou RMO (Replication Management Objects). Para obter informações sobre as condições nas quais os artigos podem ser removidos e se a remoção de um artigo requer um novo instantâneo ou a reinicialização de assinaturas, consulte [Adicionar e remover artigos de publicações existentes](add-articles-to-and-drop-articles-from-existing-publications.md).  
  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Os artigos podem ser excluídos de forma programática usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual o artigo pertence.  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>Para excluir um artigo de um instantâneo ou publicação transacional  
  
1.  Execute [sp_droparticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql) para excluir um artigo, especificado por **@article** , de uma publicação, especificado por **@publication** . Especifique um valor de **1** para **@force_invalidate_snapshot** .  
  
2.  (Opcional) Para remover inteiramente o objeto publicado de um banco de dados, execute o comando `DROP <objectname>` no Publicador do banco de dados de publicação.  
  
#### <a name="to-delete-an-article-from-a-merge-publication"></a>Para excluir um artigo de uma publicação de mesclagem  
  
1.  Execute [sp_dropmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql) para excluir um artigo, especificado por **@article** , de uma publicação, especificado por **@publication** . Se necessário, especifique um valor de **1** para **@force_invalidate_snapshot** e um valor de **1** para **@force_reinit_subscription** .  
  
2.  (Opcional) Para remover inteiramente o objeto publicado de um banco de dados, execute o comando `DROP <objectname>` no Publicador do banco de dados de publicação.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo a seguir exclui um artigo da publicação transacional. Como essa alteração invalida o instantâneo existente, um valor de **1** é especificado para o parâmetro **@force_invalidate_snapshot** .  
  
 [!code-sql[HowTo#sp_droparticle](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droparticle)]  
  
 O exemplo a seguir exclui dois artigos de uma publicação de mesclagem. Como essas alterações invalidam o instantâneo existente, um valor de **1** é especificado para o parâmetro **@force_invalidate_snapshot** .  
  
 [!code-sql[HowTo#sp_dropmergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergearticle)]
 [!code-sql[HowTo#sp_dropmergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergearticles.sql#sp_dropmergearticle)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode excluir artigos programaticamente usando o RMO (Replication Management Objects). As classes RMO que você usa para excluir um artigo dependem do tipo de publicação a que o artigo pertence.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>Para excluir um artigo que pertence a uma publicação de instantâneo ou transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransArticle> .  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para se certificar de que o artigo existe. Se o valor desta propriedade for `false`, as propriedades do artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A>.  
  
7.  Feche todas as conexões.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>Para excluir um artigo que pertence a uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeArticle> .  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para se certificar de que o artigo existe. Se o valor desta propriedade for `false`, as propriedades do artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A>.  
  
7.  Feche todas as conexões.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar e remover artigos de publicações existentes](add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
