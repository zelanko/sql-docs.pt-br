---
title: Gerenciar partições de uma publicação de mesclagem com filtros com parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- partitions [SQL Server replication]
- merge replication partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], partition management
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b8b9cc6b2328e24758404cae5a88f21656fb7631
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115878"
---
# <a name="manage-partitions-for-a-merge-publication-with-parameterized-filters"></a>Gerenciar partições para uma publicação de mesclagem com filtros com parâmetros
  Este tópico descreve como gerenciar partições para uma publicação de mesclagem com filtros com parâmetros no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o RMO (Replication Management Objects). Filtros de linha com parâmetros podem ser usados para gerar partições não sobrepostas. Essas partições podem ser restringidas de forma que só uma assinatura receba uma determinada partição. Nesses casos, um grande número de assinantes resultará em um grande número de partições, que por sua vez, exige um número igual de instantâneos particionados. Para saber mais, confira [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para gerenciar partições para uma publicação de mesclagem com filtros com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Se você fizer um script de topologia de replicação, o que é recomendado, os scripts de publicação contêm as chamadas de procedimento armazenado para criar partições de dados. O script fornece uma referência para as partições criadas e um modo para recriar uma ou mais partições, caso seja necessário. Para obter mais informações, consulte [Scripting Replication](../scripting-replication.md).  
  
-   Quando uma publicação tiver filtros com parâmetros que geram assinaturas com partições não sobrepostas ou se uma assinatura específica estiver perdida e necessitar de nova criação, faça o seguinte: remova a partição que estava com assinatura, recrie a assinatura e, em seguida, recrie a partição. Para saber mais, confira [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md). A replicação gera scripts de criação para as partições de Assinante existentes quando um script de criação de publicação é gerado. Para obter mais informações, consulte [Scripting Replication](../scripting-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Gerencie as partições na página **Partições de dados** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md). Nessa página você pode: criar e excluir partições, permitir que Assinantes iniciem a geração e entrega de instantâneo, gerar instantâneos para uma ou mais partições e limpar instantâneos.  
  
#### <a name="to-create-a-partition"></a>Para criar uma partição  
  
1.  Na página **Partições de Dados** da caixa de diálogo **Propriedades da Publicação – \<Publication>**, clique em **Adicionar**.  
  
2.  Na caixa de diálogo **Adicionar Partição de Dados** coloque o valor para **HOST_NAME()** e/ou o valor **SUSER_SNAME()** associado com a partição que você quer criar.  
  
3.  Especifique, opcionalmente, um cronograma para atualizar instantâneos:  
  
    1.  Selecione **Agendar o Snapshot Agent para que esta partição seja executada no(s) seguinte(s) horário(s):**  
  
    2.  Aceite o cronograma padrão para atualizar instantâneos ou clique em **Alterar** para especificar um cronograma diferente.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-partition"></a>Para excluir uma partição  
  
1.  Na página **Partições de Dados** , selecione uma partição na grade.  
  
2.  Clique em **Excluir**.  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>Para permitir que os Assinantes iniciem a geração e entrega de instantâneo  
  
1.  Na página **Partições de Dados** selecione **Definir automaticamente uma partição e gerar um instantâneo, se necessário, quando um novo Assinante tentar sincronizar**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-generate-a-snapshot-for-a-partition"></a>Para gerar um instantâneo para uma partição  
  
1.  Na página **Partições de Dados** , selecione uma partição na grade.  
  
2.  Clique em **Gerar os instantâneos selecionados agora**  
  
#### <a name="to-clean-up-a-snapshot-for-a-partition"></a>Limpar um instantâneo para uma partição  
  
1.  Na página **Partições de Dados** , selecione uma partição na grade.  
  
2.  Clique em **Limpar os instantâneos existentes**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Para administrar melhor uma publicação com filtros com parâmetros, você pode enumerar programaticamente as partições existentes que usam procedimentos armazenados de replicação. Você também pode criar e excluir partições existentes. Podem ser obtidas as seguintes informações a respeito das partições existentes:  
  
-   Como uma partição é filtrada (usando [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql) ou [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql)).  
  
-   O nome do trabalho que gera um instantâneo particionado.  
  
-   A última vez que um trabalho de instantâneo particionado foi executado.  
  
 Enquanto a segunda parte do instantâneo de duas partes pode ser gerada sob solicitação quando uma nova assinatura for incializada, os procedimentos abaixo permitem a você controlar o modo que é gerado o instantâneo e como pré-gerar esse instantâneo quando for mais conveniente. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md).  
  
#### <a name="to-view-information-on-existing-partitions"></a>Para exibir informações sobre partições existentes  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql). Especifique o nome da publicação para **@publication**. (Opcional) Especifique **@suser_sname** ou **@host_name** para retornar somente informações baseadas em um único critério de filtragem.  
  
#### <a name="to-define-a-new-partition-and-generate-a-new-partitioned-snapshot"></a>Para definir uma partição nova e gerar um instantâneo particionado novo  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql). Especifique o nome da publicação para **@publication**e o valor com parâmetros que define a partição para um dos seguintes:  
  
    -   **@suser_sname** – quando o filtro com parâmetros estiver definido pelo valor retornado por [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql).  
  
    -   **@host_name** – quando o filtro com parâmetros estiver definido pelo valor retornado por [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql).  
  
2.  Crie e inicialize o instantâneo com parâmetros para esta partição nova. Para obter mais informações, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
#### <a name="to-delete-a-partition"></a>Para excluir uma partição  
  
1.  No Publicador do banco de dados de publicação, execute [sp_dropmergepartition &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql). Especifique o nome da publicação para **@publication** e o valor com parâmetros que define a partição para um dos seguintes:  
  
    -   **@suser_sname** – quando o filtro com parâmetros estiver definido pelo valor retornado por [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql).  
  
    -   **@host_name** – quando o filtro com parâmetros estiver definido pelo valor retornado por [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql).  
  
     Isso também remove o trabalho de instantâneo e qualquer arquivo de instantâneo para a partição.  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Para gerenciar melhor uma publicação com filtros com parâmetros, você pode criar programaticamente novas partições de Assinante, enumerar as partições de Assinante existentes e excluir partições de Assinante usando RMO (Replication Management Objects). Para obter informações sobre como criar partições de Assinante, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). As informações a seguir a respeito das partições existentes podem ser obtidas:  
  
-   A função do valor e da filtragem sobre a qual a partição está baseada.  
  
-   O nome do trabalho que gera um instantâneo com parâmetros para o Assinante.  
  
-   A última vez em que um trabalho de instantâneo com parâmetros foi executado.  
  
#### <a name="to-view-information-on-existing-partitions"></a>Para exibir informações sobre partições existentes  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> . Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criada na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> e passe o resultado para uma matriz de objetos <xref:Microsoft.SqlServer.Replication.MergePartition> .  
  
5.  Para cada objeto <xref:Microsoft.SqlServer.Replication.MergePartition> na matriz, obtenha as propriedades de interesse.  
  
#### <a name="to-delete-existing-partitions"></a>Para excluir partições existentes  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> . Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criada na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> e passe o resultado para uma matriz de objetos <xref:Microsoft.SqlServer.Replication.MergePartition> .  
  
5.  Para cada objeto <xref:Microsoft.SqlServer.Replication.MergePartition> na matriz, determine se a partição deve ser excluída. Normalmente, essa decisão se baseia no valor da propriedade <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> ou da propriedade <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> .  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> no objeto <xref:Microsoft.SqlServer.Replication.MergePublication> da etapa 2. Passe o objeto <xref:Microsoft.SqlServer.Replication.MergePartition> da etapa 5.  
  
7.  Repita a etapa 6 para cada partição excluída.  
  
## <a name="see-also"></a>Consulte também  
 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
