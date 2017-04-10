---
title: "Informa&#231;&#245;es do Publicador, Lista de Observa&#231;&#227;o da Assinatura (publica&#231;&#227;o de mesclagem, SQL Server 2005 e vers&#245;es posteriores) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1"
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Informa&#231;&#245;es do Publicador, Lista de Observa&#231;&#227;o da Assinatura (publica&#231;&#227;o de mesclagem, SQL Server 2005 e vers&#245;es posteriores)
  O **lista de observação da assinatura** guia está disponível para distribuidores executando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores; ele é destinado para exibir informações sobre assinaturas de todas as publicações disponíveis no publicador selecionado. Você pode filtrar a lista de assinaturas para ver erros, avisos e qualquer assinatura de desempenho insatisfatório. Este guia fornece um único local para o administrador monitorar todas as atividades de replicação em um publicador: o Replication Monitor exibe todas as assinaturas que exigem atenção, com base no tipo de replicação selecionado e a opção escolhida no **Mostrar** caixa de listagem suspensa. Como os itens mostrados nessa guia são baseados no status atual e no desempenho, as assinaturas serão exibidas nessa página somente se corresponderem à opção da caixa de listagem **Mostrar** naquele momento.  
  
## Opções  
 Para obter informações mais detalhadas e tarefas relacionadas a uma assinatura, clique com o botão direito do mouse na linha dessa assinatura e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas** .  
  
-   **Selecionar Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas** .  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro** .  
  
-   **Limpar Filtro**: limpe as configurações de filtro da grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Mostrar Assinaturas Mescladas**  
 Selecione o tipo de assinatura (transacional, instantâneo ou mesclagem) a ser exibida para o Publicador selecionado.  
  
 **Mostrar**  
 Selecione os estados de assinatura a serem exibidos para o tipo de assinatura selecionado. Por exemplo, você pode optar por exibir somente as assinaturas que tiverem um erro.  
  
 **Status**  
 O status de cada assinatura que é determinado pelo status do Merge Agent.  
  
 Por padrão, a grade que contém informações de assinatura é classificada pelo **Status** coluna (e, em seguida, classificados pelo **desempenho** coluna para essas assinaturas com o mesmo status). A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, os erros são sempre mostrados na parte superior da grade).  
  
-   Erro  
  
-   Desempenho crítico  
  
-   Mesclagem de execução longa  
  
-   Expirando em breve/Expirado  
  
-   Assinatura não inicializada  
  
-   Tentando novamente comando com falha  
  
-   Sincronizando  
  
-   Não sincronizando  
  
 A ordem de classificação também determina qual valor será exibido se uma determinada assinatura estiver em mais de um estado. Por exemplo, se uma assinatura tiver um erro e expirar em breve, a coluna **Status** exibirá **Erro**.  
  
 Os valores de status **desempenho crítico**, **mesclagem de execução longa**, **expirando em breve/expirado**, e **assinatura não inicializada** são avisos. Quando um aviso for exibido, o **Status** coluna também exibe se um agente está sincronizando. Por exemplo, o status poderia ser **sincronizando, desempenho crítico**.  
  
 Os valores de status **expirando em breve/expirado** e **mesclagem de execução longa** podem ser exibidos somente se os limites são definidos. O valor de status **desempenho crítico** podem ser exibidas somente depois de cinco sincronizações de assinaturas com o mesmo tipo de conexão (discada ou LAN). Para obter informações sobre medidas de desempenho e definir limites, consulte [monitorar o desempenho com o Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) e [definir limites e avisos no Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Assinatura**  
 O nome de cada assinatura, no formato:*SubscriberName: SubscriptionDatabaseName*.  
  
 **Nome Amigável**  
 A descrição de cada assinatura. A descrição é inserida no **Propriedades de assinatura** caixa de diálogo ou especificada com o **@description** parâmetro do [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) ou [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Os usuários geralmente usam a descrição como um "nome amigável" ou apelido para a assinatura.  
  
 **Publicação**  
 O nome da publicação com a qual uma assinatura é sincronizada, no formato: *PublicationDatabaseName: PublicationName*.  
  
 **Desempenho**  
 A classificação de desempenho de cada assinatura, com base nas medidas mais recentes de taxa de entrega calculadas pelo Replication Monitor. A classificação é determinada comparando o desempenho de uma assinatura individual com o desempenho histórico médio de assinaturas com a publicação que tem o mesmo tipo de conexão (discada ou LAN). O Replication Monitor exibe um valor após a ocorrência de cinco sincronizações com 50 ou mais alterações cada, no mesmo tipo de conexão. Se houver menos de cinco sincronizações com 50 ou mais alterações ou se a sincronização mais recente tiver menos de 50 alterações, essa coluna ficará em branco.  
  
> [!NOTE]  
>  Desempenho é baseado no tipo de conexão exibido na **conexão** coluna; portanto, é possível para uma assinatura com uma taxa de entrega mais baixa para exibir uma classificação de desempenho melhor que a outra assinatura se a primeira assinatura é sincronizada em uma conexão mais lenta.  
  
 A classificação de desempenho é um dos seguintes valores:  
  
-   Excelente  
  
-   Bom  
  
-   Razoável  
  
-   Fraco  
  
 Para obter mais informações sobre como as avaliações de desempenho são definidas e como os limites de desempenho são configurados, consulte [monitorar o desempenho com o Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Taxa de Entrega**  
 O número de linhas por segundo processado pelo Merge Agent.  
  
 **Última Sincronização**  
 A hora da última execução do Merge Agent. As alterações podem ou não ter sido processadas durante essa sincronização. Se a sincronização estiver em progresso, um valor da porcentagem concluída será exibido.  
  
 **Duration**  
 A quantidade de tempo de execução do Merge Agent durante a última sincronização. O tempo representa o tempo decorrido, se o Merge Agent estiver sendo executado no momento, e o tempo total, se o Merge Agent foi sincronizado anteriormente.  
  
 **Conexão**  
 O tipo de conexão entre o Assinante e o Editor. Os valores possíveis são **LAN**, **dial-up**, e **Internet**. O **Internet** valor é exibido se a assinatura usar sincronização da Web.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para um publicador & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Sincronização da Web para replicação de mesclagem.](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  