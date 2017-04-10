---
title: "Gerenciar parti&#231;&#245;es para uma publica&#231;&#227;o de mesclagem com filtros com par&#226;metros | Microsoft Docs"
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
  - "partitions [SQL Server replication]"
  - "merge replication partitions [SQL Server replication], SQL Server Management Studio"
  - "filtros com parâmetros [replicação do SQL Server], gerenciamento de partição"
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Gerenciar parti&#231;&#245;es para uma publica&#231;&#227;o de mesclagem com filtros com par&#226;metros
  Este tópico descreve como gerenciar partições para uma publicação de mesclagem com filtros com parâmetros no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o RMO (Replication Management Objects). Filtros de linha com parâmetros podem ser usados para gerar partições não sobrepostas. Essas partições podem ser restringidas de forma que só uma assinatura receba uma determinada partição. Nesses casos, um grande número de assinantes resultará em um grande número de partições, que por sua vez, exige um número igual de instantâneos particionados. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para gerenciar partições para uma publicação de mesclagem com filtros com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Se você fizer um script de topologia de replicação, o que é recomendado, os scripts de publicação contêm as chamadas de procedimento armazenado para criar partições de dados. O script fornece uma referência para as partições criadas e um modo para recriar uma ou mais partições, caso seja necessário. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
-   Quando uma publicação tiver filtros com parâmetros que geram assinaturas com partições não sobrepostas ou se uma assinatura específica estiver perdida e necessitar de nova criação, faça o seguinte: remova a partição que estava com assinatura, recrie a assinatura e, em seguida, recrie a partição. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md). A replicação gera scripts de criação para as partições de Assinante existentes quando um script de criação de publicação é gerado. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Gerenciar partições no **partições de dados** página de **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Nessa página você pode: criar e excluir partições, permitir que Assinantes iniciem a geração e entrega de instantâneo, gerar instantâneos para uma ou mais partições e limpar instantâneos.  
  
#### Para criar uma partição  
  
1.  No **partições de dados** página o **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **Adicionar**.  
  
2.  Na **Adicionar partição de dados** caixa de diálogo, digite um valor para o **HOST_NAME ()** e/ou **suser_sname ()** valor associado à partição que você deseja criar.  
  
3.  Especifique, opcionalmente, um cronograma para atualizar instantâneos:  
  
    1.  Selecione **agendamento do agente de instantâneo desta partição ser executada às vezes a seguir**  
  
    2.  Aceite o cronograma padrão para atualizar instantâneos ou clique em **Alterar** para especificar um cronograma diferente.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para excluir uma partição  
  
1.  Na página **Partições de Dados** , selecione uma partição na grade.  
  
2.  Clique em **Excluir**.  
  
#### Para permitir que os Assinantes iniciem a geração e entrega de instantâneo  
  
1.  Na página **Partições de Dados** selecione **Definir automaticamente uma partição e gerar um instantâneo, se necessário, quando um novo Assinante tentar sincronizar**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para gerar um instantâneo para uma partição  
  
1.  Na página **Partições de Dados** , selecione uma partição na grade.  
  
2.  Clique em **Gerar os instantâneos selecionados agora**  
  
#### Limpar um instantâneo para uma partição  
  
1.  Na página **Partições de Dados** , selecione uma partição na grade.  
  
2.  Clique em **Limpar os instantâneos existentes**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Para administrar melhor uma publicação com filtros com parâmetros, você pode enumerar programaticamente as partições existentes que usam procedimentos armazenados de replicação. Você também pode criar e excluir partições existentes. Podem ser obtidas as seguintes informações a respeito das partições existentes:  
  
-   Como uma partição é filtrada (usando [SUSER_SNAME & #40. O Transact-SQL e 41;](../../../t-sql/functions/suser-sname-transact-sql.md) ou [HOST_NAME & #40. Transact-SQL & 41;](../../../t-sql/functions/host-name-transact-sql.md)).  
  
-   O nome do trabalho que gera um instantâneo particionado.  
  
-   A última vez que um trabalho de instantâneo particionado foi executado.  
  
 Enquanto a segunda parte do instantâneo de duas partes pode ser gerada sob solicitação quando uma nova assinatura for incializada, os procedimentos abaixo permitem a você controlar o modo que é gerado o instantâneo e como pré-gerar esse instantâneo quando for mais conveniente. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
#### Para exibir informações sobre partições existentes  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergepartition & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md). Especifique o nome da publicação para **@publication**. (Opcional) Especifique **@suser_sname** ou **@host_name** para retornar somente as informações com base em um único critério de filtragem.  
  
#### Para definir uma partição nova e gerar um instantâneo particionado novo  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergepartition & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md). Especifique o nome da publicação para **@publisher**e o valor com parâmetros que define a partição para um dos seguintes:  
  
    -   **@suser_sname** - quando o filtro parametrizado é definido pelo valor retornado por [SUSER_SNAME & #40. O Transact-SQL e 41;](../../../t-sql/functions/suser-sname-transact-sql.md).  
  
    -   **@host_name** - quando o filtro parametrizado é definido pelo valor retornado por [HOST_NAME & #40. O Transact-SQL e 41;](../../../t-sql/functions/host-name-transact-sql.md).  
  
2.  Crie e inicialize o instantâneo com parâmetros para esta partição nova. Para obter mais informações, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
#### Para excluir uma partição  
  
1.  No publicador do banco de dados de publicação, execute [sp_dropmergepartition & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md). Especifique o nome da publicação para **@publication** e o valor com parâmetros que define a partição para um dos seguintes:  
  
    -   **@suser_sname** - quando o filtro parametrizado é definido pelo valor retornado por [SUSER_SNAME & #40. O Transact-SQL e 41;](../../../t-sql/functions/suser-sname-transact-sql.md).  
  
    -   **@host_name** - quando o filtro parametrizado é definido pelo valor retornado por [HOST_NAME & #40. O Transact-SQL e 41;](../../../t-sql/functions/host-name-transact-sql.md).  
  
     Isso também remove o trabalho de instantâneo e qualquer arquivo de instantâneo para a partição.  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Para gerenciar melhor uma publicação com filtros com parâmetros, você pode criar programaticamente novas partições de Assinante, enumerar as partições de Assinante existentes e excluir partições de Assinante usando RMO (Replication Management Objects). Para obter informações sobre como criar partições de Assinante, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). As informações a seguir a respeito das partições existentes podem ser obtidas:  
  
-   A função do valor e da filtragem sobre a qual a partição está baseada.  
  
-   O nome do trabalho que gera um instantâneo com parâmetros para o Assinante.  
  
-   A última vez em que um trabalho de instantâneo com parâmetros foi executado.  
  
#### Para exibir informações sobre partições existentes  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> classe. Definir o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> método e passar o resultado em uma matriz de <xref:Microsoft.SqlServer.Replication.MergePartition> objetos.  
  
5.  Para cada <xref:Microsoft.SqlServer.Replication.MergePartition> de objeto na matriz, obtenha as propriedades de seu interesse.  
  
#### Para excluir partições existentes  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> classe. Definir o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> método e passar o resultado em uma matriz de <xref:Microsoft.SqlServer.Replication.MergePartition> objetos.  
  
5.  Para cada <xref:Microsoft.SqlServer.Replication.MergePartition> de objeto na matriz, determine se a partição deve ser excluída. Essa decisão normalmente com base no valor da <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> propriedade ou o <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> propriedade.  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> método o <xref:Microsoft.SqlServer.Replication.MergePublication> objeto da etapa 2. Passar o <xref:Microsoft.SqlServer.Replication.MergePartition> objeto da etapa 5.  
  
7.  Repita a etapa 6 para cada partição excluída.  
  
## Consulte também  
 [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Instantâneos para publicações de mesclagem com filtros com parâmetros](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  