---
title: "Visualizar e modificar propriedades de artigos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "sp_changearticle"
  - "sp_helparticle"
  - "exibindo propriedades de replicação"
  - "sp_changemergearticle"
  - "sp_helpmergearticle"
  - "modificando propriedades de replicação, artigos"
  - "artigos [replicação SQL Server], modificando"
  - "artigos [replicação SQL Server], propriedades"
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Visualizar e modificar propriedades de artigos
  Este tópico descreve como exibir e modificar propriedades do artigo no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o RMO (Replication Management Objects).  
  
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
  
-   Depois que uma publicação é criada, algumas alterações de propriedade requerem um novo instantâneo. Se uma publicação tiver assinaturas, algumas alterações também exigirão que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) e [Adicionar e descartar artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exibir e modificar propriedades do artigo no **Propriedades de publicação - \< publicação>** caixa de diálogo, que está disponível em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
-   A página **Geral** inclui o nome e descrição da publicação, o nome do banco de dados, o tipo da publicação, e as configurações para expiração da assinatura.  
  
-   A página **Artigos** corresponde à página **Artigos** no Assistente para Nova Publicação. Use essa página para adicionar e excluir artigos e para alterar propriedades e filtros de coluna para artigos.  
  
-   A página **Filtrar Linhas** corresponde à página **Filtrar Linhas de Tabela** no Assistente para Nova Publicação. Use essa página para adicionar, editar e excluir filtros de linhas estáticas para todos os tipos de publicações, e para adicionar, editar e excluir filtros de linhas com parâmetros e associar filtros para publicações de mesclagem.  
  
-   A página **Instantâneo** permite que você especifique o formato e o local do instantâneo, se o instantâneo deve estar compactado e scripts para serem executados antes e depois que o instantâneo for aplicado.  
  
-   O **instantâneo de FTP** página (para instantâneo e publicações transacionais e publicações de mesclagem para Publicadores executando versões anteriores do SQL Server 2005) permite que você especifique se os assinantes podem baixar os arquivos de instantâneo por meio de protocolo FTP (File Transfer).  
  
-   O **instantâneo de FTP e Internet** página (para publicações de mesclagem de Publicadores executando o SQL Server 2005 ou posterior) permite que você especifique se os assinantes podem baixar os arquivos de instantâneo por FTP, e se os assinantes podem sincronizar assinaturas através de HTTPS.  
  
-   A página **Opções de Assinatura** permite que você possa definir um número de opções que se aplicam à todas as assinaturas. As opções diferem dependendo do tipo de publicação.  
  
-   A página **Lista de Acesso à Publicação** permite que você especifique quais logons e grupos podem acessar uma publicação.  
  
-   A página **Segurança do Agente** permite que você acesse as configurações para as contas sob as quais os seguintes agentes executam e fazem conexões com os computadores em uma topologia de replicação: O Agente de Instantâneo para todas as publicações; o Log Reader Agent para todas as publicações transacionais e o Queue Reader Agent para publicações transacionais que permitem assinaturas de atualização enfileiradas.  
  
-   O **partições de dados** página (para publicações de mesclagem de Publicadores executando o SQL Server 2005 ou posterior) permite que você especifique se os assinantes de publicações com filtros com parâmetros podem solicitar um instantâneo se não houver um disponível. Ele também permite que você gere instantâneos para uma ou mais partições uma vez ou em uma agenda recorrente.  
  
#### Para visualizar e modificar as propriedades do artigo  
  
1.  Sobre o **artigos** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um artigo e, em seguida, clique em **Propriedades do artigo**.  
  
2.  Selecione quais alterações da propriedade dos artigos devem ser aplicadas a:  
  
    -   Clique em **definir propriedades de realçado \< ObjectType> artigo** para iniciar o **Propriedades do artigo - \< ObjectName>** caixa de diálogo; propriedade as alterações feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel do objeto no **artigos** página.  
  
    -   Clique em **definir propriedades de todos os \< ObjectType> artigos**, para iniciar o **Propriedades para todos os \< ObjectType> artigos** caixa de diálogo; propriedade as alterações feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo no painel objeto o **artigos** página, incluindo os ainda não foram selecionados para publicação.  
  
        > [!NOTE]  
        >  Alterações de propriedade feitas a **Propriedades para todos os \< ObjectType> artigos** caixa de diálogo Substituir qualquer feitas anteriormente no **Propriedades do artigo - \< ObjectName>** caixa de diálogo. Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
3.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
4.  Clique em **OK** sobre o **Propriedades de publicação - \< publicação>** caixa de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 É possível modificar artigos e retornar suas propriedades programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual o artigo pertence.  
  
#### Para exibir as propriedades de um artigo que pertence a um instantâneo ou publicação transacional  
  
1.  Executar [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md), especificando o nome da publicação para o **@publication** parâmetro e o nome do artigo para a **@article** parâmetro. Se você não especificar **@article**, serão retornadas informações de todos os artigos na publicação.  
  
2.  Executar [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) para artigos de tabela listar todas as colunas disponíveis na tabela base.  
  
#### Para modificar as propriedades de um artigo que pertence a um instantâneo ou publicação transacional  
  
1.  Executar [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md), especificando a propriedade do artigo que está sendo alterada no **@property** parâmetro e o novo valor dessa propriedade no **@value** parâmetro.  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, você também deve especificar um valor de **1** para **@force_invalidate_snapshot**, e se a alteração exigir que os assinantes sejam reinicializados, você também deve especificar um valor de **1** para **@force_reinit_subscription**. Para obter mais informações sobre as propriedades que, quando alteradas, requerem um novo instantâneo ou reinicialização, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
#### Para exibir as propriedades de um artigo que pertence a uma publicação de mesclagem  
  
1.  Executar [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md), especificando o nome da publicação para o **@publication** parâmetro e o nome do artigo para a **@article** parâmetro. Se você não especificar esses parâmetros, serão retornadas informações de todos os artigos em uma publicação ou no publicador.  
  
2.  Executar [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) para artigos de tabela listar todas as colunas disponíveis na tabela base.  
  
#### Para modificar as propriedades de um artigo que pertence a uma publicação de mesclagem  
  
1.  Executar [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando a propriedade do artigo que está sendo alterada no **@property** parâmetro e o novo valor dessa propriedade no **@value** parâmetro.  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, você também deve especificar um valor de **1** para **@force_invalidate_snapshot**, e se a alteração exigir que os assinantes sejam reinicializados, você também deve especificar um valor de **1** para **@force_reinit_subscription**. Para obter mais informações sobre as propriedades que, quando alteradas, requerem um novo instantâneo ou reinicialização, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
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
  
#### Para exibir ou modificar propriedades de um artigo que pertence a uma publicação de instantâneo ou transacional  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransArticle> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Propriedades.  
  
4.  Defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.TransArticle> propriedades que podem ser definidas.  
  
7.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
#### Para exibir ou modificar propriedades de um artigo que pertence a uma publicação de mesclagem  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeArticle> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Propriedades.  
  
4.  Defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de artigo na etapa 3 foram definidas incorretamente ou o artigo não existe.  
  
6.  (Opcional) Para alterar propriedades, defina um novo valor para uma da <xref:Microsoft.SqlServer.Replication.MergeArticle> propriedades que podem ser definidas.  
  
7.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Esse exemplo altera um artigo de mesclagem para especificar o manipulador de lógica de negócios usado pelo artigo.  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## Consulte também  
 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  