---
title: "Visualizar e modificar as propriedades da publica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exibindo propriedades de replicação"
  - "modificando propriedades de replicação, artigos"
  - "artigos [replicação SQL Server], modificando"
  - "publicações [replicação do SQL Server], propriedade"
  - "artigos [replicação SQL Server], propriedades"
  - "modificando propriedades de replicação, publicações"
  - "publicações [replicação do SQL Server], modificando"
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Visualizar e modificar as propriedades da publica&#231;&#227;o
  Este tópico descreve como exibir e modificar propriedades de publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para exibir e modificar propriedades de publicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Algumas propriedades não podem ser modificadas após uma publicação ter sido criada, e outras não podem ser modificadas se houverem assinaturas na publicação. As propriedades que não podem ser definidas são exibidas como somente leitura.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Depois que uma publicação é criada, algumas alterações de propriedade requerem um novo instantâneo. Se uma publicação tiver assinaturas, algumas alterações também exigirão que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) e [Adicionar e descartar artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exibir e modificar propriedades de publicação na **Propriedades de publicação - \< publicação>** caixa de diálogo, que está disponível em [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e o Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
 O **Propriedades de publicação - \< publicação>** caixa de diálogo inclui as seguintes páginas:  
  
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
  
#### Para visualizar e modificar propriedades de publicação no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Uma publicação de atalho e, em seguida, clique em **propriedades**.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
#### Para visualizar e modificar propriedades de publicação no Replication Monitor  
  
1.  Expanda um Grupo do publicador no painel esquerdo do Replication Monitor e, depois, expanda um Publicador.  
  
2.  Uma publicação de atalho e, em seguida, clique em **propriedades**.  
  
3.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Publicações podem ser modificadas e suas propriedades retornadas programaticamente usando-se procedimentos armazenados de replicação. Os procedimentos armazenados usados dependerão do tipo de publicação.  
  
#### Para visualizar as propriedades de uma publicação de instantâneo ou transacional  
  
1.  Executar [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md), especificando o nome da publicação para o **@publication** parâmetro. Se você não especificar esse parâmetro, as informações sobre todas as publicações no Publicador serão retornadas.  
  
#### Para alterar as propriedades de uma publicação de instantâneo ou transacional  
  
1.  Executar [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando a propriedade de publicação para alterar o **@property** parâmetro e o novo valor dessa propriedade no **@value** parâmetro.  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, você também deve especificar um valor de **1** para **@force_invalidate_snapshot**, e se a alteração exigir que os assinantes sejam reinicializados, você deve especificar um valor de **1** para **@force_reinit_subscription**. Para obter mais informações sobre as propriedades que, quando alteradas, requerem um novo instantâneo ou reinicialização, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
#### Para visualizar as propriedades de uma publicação de mesclagem  
  
1.  Executar [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando o nome da publicação para o **@publication** parâmetro. Se você não especificar esse parâmetro, as informações sobre todas as publicações no Publicador serão retornadas.  
  
#### Para alterar as propriedades de uma publicação de mesclagem  
  
1.  Executar [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando a propriedade de publicação que está sendo alterada no **@property** parâmetro e o novo valor dessa propriedade no **@value** parâmetro.  
  
    > [!NOTE]  
    >  Se a alteração exigir a geração de um novo instantâneo, você também deve especificar um valor de **1** para **@force_invalidate_snapshot**, e se a alteração exigir que os assinantes sejam reinicializados, você deve especificar um valor de **1** para **@force_reinit_subscription** para obter mais informações sobre as propriedades que, quando alteradas, requerem um novo instantâneo ou reinicialização, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
#### Para visualizar as propriedades de um instantâneo  
  
1.  Executar [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), especificando o nome da publicação para o **@publication** parâmetro.  
  
#### Para alterar as propriedades de um instantâneo  
  
1.  Executar [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), especificando uma ou mais propriedades de instantâneo novas para os parâmetros de instantâneo apropriados.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo de replicação transacional retorna as propriedades da publicação.  
  
 [!code-sql[HowTo#sp_helppublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_1.sql)]  
  
 Esse exemplo de replicação transacional desabilita a replicação de esquema para a publicação.  
  
 [!code-sql[HowTo#sp_changepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_2.sql)]  
  
 Esse exemplo de replicação de mesclagem retorna as propriedades da publicação.  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_3.sql)]  
  
 Esse exemplo de replicação de mesclagem desabilita a replicação de esquema para a publicação.  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_4.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode modificar as publicações e acessar suas propriedades programaticamente, usando o RMO (Replication Management Objects). As classes RMO que você usa para visualizar ou modificar as propriedades da publicação, dependem do tipo da publicação.  
  
#### Para visualizar ou modificar as propriedades de um instantâneo ou publicação transacional  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPublication> classe, defina o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  (Opcional) Para alterar as propriedades, defina um novo valor para uma ou mais propriedades definíveis. Use o operador AND lógico (**&** no Microsoft Visual c# e **e** no Microsoft Visual Basic) para determinar se um determinado <xref:Microsoft.SqlServer.Replication.PublicationAttributes> valor está definido para o <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade. Use o operador OR lógica inclusiva (**|** no Visual c# e **ou** no Visual Basic) e o operador OR lógica exclusiva (**^** no Visual c# e **Xor** no Visual Basic) para alterar o <xref:Microsoft.SqlServer.Replication.PublicationAttributes> valores para o <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade.  
  
5.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
#### Para visualizar ou modificar as propriedades de uma publicação de mesclagem  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> de classe, defina o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  (Opcional) Para alterar as propriedades, defina um novo valor para uma ou mais propriedades definíveis. Use o operador AND lógico (**&** no Visual c# e **e** no Visual Basic) para determinar se um determinado <xref:Microsoft.SqlServer.Replication.PublicationAttributes> valor está definido para o <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade. Use o operador OR lógica inclusiva (**|** no Visual c# e **ou** no Visual Basic) e o operador OR lógica exclusiva (**^** no Visual c# e **Xor** no Visual Basic) para alterar o <xref:Microsoft.SqlServer.Replication.PublicationAttributes> valores para o <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propriedade.  
  
5.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo define atributos de publicação para uma publicação transacional. As alterações são armazenadas em cache até que sejam explicitamente enviadas ao servidor.  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 Esse exemplo desabilita a replicação DDL para uma publicação de mesclagem.  
  
 [!code-csharp[HowTo#rmo_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## Consulte também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Adicionar e remover artigos de uma publicação & #40. SQL Server Management Studio e 41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)   
 [Exibir informações e executar tarefas para uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Visualizar e modificar propriedades de artigos](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  