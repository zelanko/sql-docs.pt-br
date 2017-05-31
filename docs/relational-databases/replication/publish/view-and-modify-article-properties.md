---
title: Exibir e modificar propriedades de artigos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changearticle
- sp_helparticle
- viewing replication properties
- sp_changemergearticle
- sp_helpmergearticle
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- articles [SQL Server replication], properties
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7dd32148c10d940808986a58e78c6528bc772d9b
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="view-and-modify-article-properties"></a>Visualizar e modificar propriedades de artigos
  Este tópico descreve como exibir e modificar propriedades do artigo no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para exibir e modificar as propriedades do artigo, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Algumas propriedades não podem ser modificadas após uma publicação ter sido criada, e outras não podem ser modificadas se houverem assinaturas na publicação. As propriedades que não podem ser definidas são exibidas como somente leitura.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Depois que uma publicação é criada, algumas alterações de propriedade requerem um novo instantâneo. Se uma publicação tiver assinaturas, algumas alterações também exigirão que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) e [Add Articles to and Drop Articles from Existing Publications](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exibir e modificar propriedades do artigo na caixa de diálogo **Propriedades de Publicação – \<Publicação>**, disponível no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
-   A página **Geral** inclui o nome e descrição da publicação, o nome do banco de dados, o tipo da publicação, e as configurações para expiração da assinatura.  
  
-   A página **Artigos** corresponde à página **Artigos** no Assistente para Nova Publicação. Use essa página para adicionar e excluir artigos e para alterar propriedades e filtros de coluna para artigos.  
  
-   A página **Filtrar Linhas** corresponde à página **Filtrar Linhas de Tabela** no Assistente para Nova Publicação. Use essa página para adicionar, editar e excluir filtros de linhas estáticas para todos os tipos de publicações, e para adicionar, editar e excluir filtros de linhas com parâmetros e associar filtros para publicações de mesclagem.  
  
-   A página **Instantâneo** permite que você especifique o formato e o local do instantâneo, se o instantâneo deve estar compactado e scripts para serem executados antes e depois que o instantâneo for aplicado.  
  
-   A página **Instantâneo FTP** (para publicações transacionais e de instantâneo e publicações de mesclagem para versões de Publicadores em execução antes do SQL Server 2005) permite que você especifique se os Assinantes podem baixar arquivos através de FTP (Protocolo de Transferência de Arquivo).  
  
-   A página **Instantâneo de FTP e Internet** (para publicações de mesclagem de Publicadores executando o SQL Server 2005 ou versões posteriores) permite que você especifique se os Assinantes podem baixar arquivos de instantâneo através de FTP, e se os Assinantes podem sincronizar as assinaturas através de HTTPS.  
  
-   A página **Opções de Assinatura** permite que você possa definir um número de opções que se aplicam à todas as assinaturas. As opções diferem dependendo do tipo de publicação.  
  
-   A página **Lista de Acesso à Publicação** permite que você especifique quais logons e grupos podem acessar uma publicação.  
  
-   A página **Segurança do Agente** permite que você acesse as configurações para as contas sob as quais os seguintes agentes executam e fazem conexões com os computadores em uma topologia de replicação: O Agente de Instantâneo para todas as publicações; o Log Reader Agent para todas as publicações transacionais e o Queue Reader Agent para publicações transacionais que permitem assinaturas de atualização enfileiradas.  
  
-   A página **Partições de Dados** (para publicações de mesclagem de Publicadores executando o SQL Server 2005 ou posterior) permite que você especifique se os Assinantes das publicações com filtros com parâmetros podem solicitar uma instantâneo, se um não estiver disponível. Ele também permite que você gere instantâneos para uma ou mais partições uma vez ou em uma agenda recorrente.  
  
#### <a name="to-view-and-modify-article-properties"></a>Para visualizar e modificar as propriedades do artigo  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione um artigo e clique em **Propriedades do Artigo**.  
  
2.  Selecione quais alterações da propriedade dos artigos devem ser aplicadas a:  
  
    -   Clique em **Definir as Propriedades do Artigo \<ObjectType> Realçado** para iniciar a caixa de diálogo **Propriedades do Artigo – \<ObjectName >**. As alterações de propriedade feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel de objetos na página **Artigos**.  
  
    -   Clique em **Definir as Propriedades de Todos os Artigos \<ObjectType>**, para iniciar a caixa de diálogo **Propriedades de Todos os Artigos \<ObjectType>**; as alterações à propriedade feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo, no painel de objetos da página **Artigos**, incluindo os ainda não selecionados para publicação.  
  
        > [!NOTE]  
        >  Alterações de propriedade feitas na caixa de diálogo **Propriedades para Todos os Artigos \<ObjectType>** substituem todas as alterações feitas anteriormente na caixa de diálogo **Propriedades do Artigo – \<ObjectName>**. Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
3.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
4.  Clique em **OK** na caixa de diálogo **Propriedades da Publicação – \<Publicação >**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 É possível modificar artigos e retornar suas propriedades programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual o artigo pertence.  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>Para exibir as propriedades de um artigo que pertence a um instantâneo ou publicação transacional  
  
1.  Execute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md), especificando o nome da publicação para o parâmetro **@publication** e o nome do artigo para o parâmetro **@article** . Se você não especificar **@article**, serão retornadas informações de todos os artigos na publicação.  
  
2.  Execute [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) para que os artigos de tabela listem todas as colunas disponíveis na tabela base.  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>Para modificar as propriedades de um artigo que pertence a um instantâneo ou publicação transacional  
  
1.  Execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md), especificando a propriedade do artigo que está sendo alterado no parâmetro **@property** e o novo valor desta propriedade no parâmetro **@value** .  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, deve-se também especificar um valor **1** para **@force_invalidate_snapshot**, e se a alteração exigir que os Assinantes sejam reinicializados, deve-se também especificar um valor **1** para **@force_reinit_subscription**. Para obter mais informações sobre as propriedades que, quando alteradas, exigem um novo instantâneo ou uma nova reinicialização, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-merge-publication"></a>Para exibir as propriedades de um artigo que pertence a uma publicação de mesclagem  
  
1.  Execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md), especificando o nome da publicação para o parâmetro **@publication** e o nome do artigo para o parâmetro **@article** . Se você não especificar esses parâmetros, serão retornadas informações de todos os artigos em uma publicação ou no publicador.  
  
2.  Execute [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) para que os artigos de tabela listem todas as colunas disponíveis na tabela base.  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-merge-publication"></a>Para modificar as propriedades de um artigo que pertence a uma publicação de mesclagem  
  
1.  Execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando a propriedade do artigo que está sendo alterado no parâmetro **@property** e o novo valor desta propriedade no parâmetro **@value** .  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, deve-se também especificar um valor **1** para **@force_invalidate_snapshot**, e se a alteração exigir que os Assinantes sejam reinicializados, deve-se também especificar um valor **1** para **@force_reinit_subscription**. Para obter mais informações sobre as propriedades que, quando alteradas, exigem um novo instantâneo ou uma nova reinicialização, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Esse exemplo de replicação transacional retorna as propriedades do artigo publicado.  
  
 [!code-sql[HowTo#sp_helptranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_1.sql)]  
  
 Esse exemplo de replicação transacional altera as opções de esquema para o artigo publicado.  
  
 [!code-sql[HowTo#sp_changetranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_2.sql)]  
  
 Esse exemplo de replicação de mesclagem retorna as propriedades do artigo publicado.  
  
 [!code-sql[HowTo#sp_helpmergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_3.sql)]  
  
 Esse exemplo de replicação de mesclagem altera as configurações de detecção de conflito para um artigo publicado.  
  
 [!code-sql[HowTo#sp_changemergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_4.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode modificar artigos e acessar suas propriedades programaticamente usando o RMO (Replication Management Objects). As classes RMO usadas para exibir ou modificar propriedades de artigo dependem do tipo de publicação a que o artigo pertence.  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>Para exibir ou modificar propriedades de um artigo que pertence a uma publicação de instantâneo ou transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransArticle>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A> e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>.  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma das propriedades <xref:Microsoft.SqlServer.Replication.TransArticle> que podem ser definidas.  
  
7.  (Opcional) Se você especificar um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-merge-publication"></a>Para exibir ou modificar propriedades de um artigo que pertence a uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeArticle>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A> e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>.  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma das propriedades <xref:Microsoft.SqlServer.Replication.MergeArticle> que podem ser definidas.  
  
7.  (Opcional) Se você especificar um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Esse exemplo altera um artigo de mesclagem para especificar o manipulador de lógica de negócios usado pelo artigo.  
  
 [!code-cs[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>Consulte também  
 [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
