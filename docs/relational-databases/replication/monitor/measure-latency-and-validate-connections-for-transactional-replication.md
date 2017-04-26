---
title: "Medir a latência e validar as conexões para a replicação transacional | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Replication Monitor, performance
- tracer tokens [SQL Server replication]
- latency [SQL Server replication]
- transactional replication, tracer tokens
- monitoring performance [SQL Server replication], tracer tokens
ms.assetid: 4addd426-7523-4067-8d7d-ca6bae4c9e34
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b2ef601ab4c3dca3b524805e9cce7798213deab9
ms.lasthandoff: 04/11/2017

---
# <a name="measure-latency-and-validate-connections-for-transactional-replication"></a>Medir a latência e validar as conexões para a replicação transacional
  Este tópico descreve como medir a latência e validar conexões para replicação transacional no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o Replication Monitor, [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou RMO (Replication Management Objects). A replicação transacional fornece o recurso do token de rastreamento, que proporciona um meio adequado para medir a latência em topologias de replicação transacional e validar as conexões entre o Publicador, o Distribuidor e os Assinantes. Um token (uma quantidade pequena de dados) é gravado no log de transações do banco de dados de publicação, marcado como se fosse uma transação replicada comum e enviado pelo sistema, permitindo um cálculo de:  
  
-   O tempo decorrido entre a confirmação de uma transação no Publicador e o comando correspondente inserido no banco de dados de distribuição no Distribuidor.  
  
-   O tempo decorrido entre um comando inserido no banco de dados de distribuição e a transação correspondente confirmada no Assinante.  
  
 Desses cálculos, você pode responder várias perguntas, enquanto incluindo:  
  
-   Quais Assinantes levam mais tempo para receber uma alteração do Publicador?  
  
-   Dos Assinantes esperados para receber o token de rastreamento quais, se houver, ainda não receberam?  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para medir a latência e validar as conexões, usando:**  
  
     [SQL Server Replication Monitor](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Os tokens de rastreamento também são úteis para confirmar um sistema, o que implica em parar todas as atividades e verificar que todos os nós tenham recebido todas as alterações pendentes. Para obter mais informações, consulte [Como confirmar uma topologia de replicação &#40;Programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
 Para usar os tokens de rastreamento, você deve utilizar versões específicas do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   O Distribuidor deve ser [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior.  
  
-   O Publicador deve ser [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior, ou ser um Editor Oracle.  
  
-   Para as assinaturas push, as estatísticas dos tokens de rastreamento são coletadas do Publicador, do Distribuidor e dos Assinantes, se o Assinante for [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 ou posterior.  
  
-   Para as assinaturas pull, as estatísticas dos tokens de rastreamento são coletadas dos Assinantes somente se o Assinante for [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior. Se o Assinante for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], somente as estatísticas do Publicador e do Distribuidor serão coletadas.  
  
 Há vários outros itens e restrições que devem ser considerados:  
  
-   Para receber um token de rastreamento, as assinaturas devem estar ativas. Uma assinatura estará ativa se ela foi inicializada.  
  
-   A reinicialização remove todos os tokens de rastreamento pendentes para as assinaturas relevantes.  
  
-   Os Assinantes recebem os tokens de rastreamento que foram criados somente após a sua sincronização inicial.  
  
-   Os tokens de rastreamento não são encaminhados pelos Assinantes de republicação.  
  
-   Depois do failover para um secundário, o Replication Monitor não pode ajustar o nome da instância de publicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e continuará exibindo informações de replicação sob o nome da instância primária original do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Depois do failover, um token de rastreamento não pode ser inserido usando o Replication Monitor; porém um token de rastreamento inserido no novo publicador usando [!INCLUDE[tsql](../../../includes/tsql-md.md)]é visível no Replication Monitor.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Replication Monitor  
 Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
#### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>Para inserir um token de rastreamento e exibir informações sobre o token  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Tokens de Rastreamento** .  
  
3.  Clique em **Inserir Rastreador**.  
  
4.  Exiba o tempo decorrido para o token de rastreamento nas seguintes colunas: **Publicador para Distribuidor**, **Distribuidor para Assinante**, **Latência Total**. Um valor de **Pendente** indica que o token não alcançou um determinado ponto.  
  
#### <a name="to-view-information-on-a-tracer-token-inserted-previously"></a>Para exibir informações sobre um token de rastreamento previamente inserido  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Tokens de Rastreamento** .  
  
3.  Selecione uma opção de tempo na lista suspensa **Tempo inserido** .  
  
4.  Exiba o tempo decorrido para o token de rastreamento nas seguintes colunas: **Publicador para Distribuidor**, **Distribuidor para Assinante**, **Latência Total**. Um valor de **Pendente** indica que o token não alcançou um determinado ponto.  
  
    > [!NOTE]  
    >  Informações de token de rastreamento são retidas para o mesmo período de tempo que outros dados históricos, os quais são governados pelo período de retenção de histórico do banco de dados de distribuição. Para obter informações sobre como alterar as propriedades do banco de dados de distribuição, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>Para publicar um token de rastreamento em uma publicação transacional  
  
1.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_helppublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). Verifique se a publicação existe e se o status é ativo.  
  
2.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_helpsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Verifique se a assinatura existe e se o status é ativo.  
  
3.  No Publicador do banco de dados de publicação, execute [sp_posttracertoken &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md), especificando **@publication**. Observe o valor do parâmetro de saída **@tracer_token_id** .  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>Para determinar a latência e validar as conexões para uma publicação transacional  
  
1.  Publique um token de rastreamento na publicação usando o procedimento anterior.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_helptracertokens &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md), especificando **@publication**. Isso retorna uma lista de todos os tokens de rastreamento publicados na publicação. Observe o **tracer_id** desejado no conjunto de resultados.  
  
3.  No Publicador do banco de dados de publicação, execute [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md), especificando **@publication** e a ID do token de rastreamento da etapa 2 para **@tracer_id**. Isso retorna informações de latência para o token de rastreamento selecionado.  
  
#### <a name="to-remove-tracer-tokens"></a>Para remover tokens de rastreamento  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helptracertokens &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md), especificando **@publication**. Isso retorna uma lista de todos os tokens de rastreamento publicados na publicação. Observe o **tracer_id** a ser excluído pelo token de rastreamento no conjunto de resultados.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md), especificando **@publication** e a ID de rastreamento a ser excluída da etapa 2 para **@tracer_id**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Esse exemplo publica um registro dos tokens de rastreamento, e usa o ID retornado do token de rastreamento publicado, para exibir as informações da latência.  
  
 [!code-sql[HowTo#sp_tracertokens](../../../relational-databases/replication/codesnippet/tsql/measure-latency-and-vali_1.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>Para publicar um token de rastreamento em uma publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como a conexão criada na etapa 1.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 3 foram definidas incorretamente ou a publicação não existe.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.TransPublication.PostTracerToken%2A>. Esse método insere um token de rastreamento no log de transações da publicação.  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>Para determinar a latência e validar as conexões para uma publicação transacional  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A> e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>; além disso, defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades do monitor da publicação na etapa 3 foram definidas incorretamente ou a publicação não existe.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A>. Converta o objeto <xref:System.Collections.ArrayList> retornado em uma matriz de objetos <xref:Microsoft.SqlServer.Replication.TracerToken>.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A>. Passe um valor <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> para um token de rastreamento da etapa 5. Isso retorna as informações da latência para o token de rastreamento selecionado como um objeto <xref:System.Data.DataSet>. Se todas as informações do token de rastreamento forem retornadas, a conexão entre o Publicador e o Distribuidor e a conexão entre o Distribuidor e o Assinante serão efetivas e a topologia de replicação estará funcionando.  
  
#### <a name="to-remove-tracer-tokens"></a>Para remover tokens de rastreamento  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A> e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>; além disso, defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades do monitor da publicação na etapa 3 foram definidas incorretamente ou a publicação não existe.  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A>. Converta o objeto <xref:System.Collections.ArrayList> retornado em uma matriz de objetos <xref:Microsoft.SqlServer.Replication.TracerToken>.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.CleanUpTracerTokenHistory%2A>. Passe um dos seguintes valores:  
  
    -   O <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> de um token de rastreamento da etapa 5. Isso exclui as informações para um token selecionado.  
  
    -   Um objeto <xref:System.DateTime>. Isso exclui as informações de todos os tokens anteriores à data e hora especificadas.  
  
  
