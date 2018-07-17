---
title: Informações da publicação, todas as assinaturas (publicação de mesclagem) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.allsubscriptions.merge.f1
ms.assetid: 0f4fa946-a0d9-4d3b-b90b-53503c40fba2
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 066fd1d4b4793a9ed183c868f05ed2b22d891c08
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358938"
---
# <a name="publication-information-all-subscriptions-merge-publication"></a>Informações da Publicação, Todas as Assinaturas (publicação de mesclagem)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A guia **Todas as Assinaturas** exibe informações sobre todas as assinaturas na publicação de mesclagem selecionada.  
  
## <a name="options"></a>Opções  
 Para obter informações mais detalhadas e tarefas relacionadas a uma assinatura, clique com o botão direito do mouse na linha dessa assinatura e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas** .  
  
-   **Selecionar Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas** .  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro** .  
  
-   **Limpar Filtro**: limpe as configurações de filtro da grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Mostrar**  
 Somente[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Selecione os estados de assinatura a serem exibidos para o tipo de assinatura selecionado. Por exemplo, você pode optar por exibir somente as assinaturas que tiverem um erro.  
  
 **Status**  
 O status de cada assinatura que é determinado pelo status do Merge Agent.  
  
 Por padrão, a grade que contém informações de assinatura é classificada pela coluna **Status** (e depois pela coluna **Desempenho** para assinaturas com o mesmo status). A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, os erros são sempre mostrados na parte superior da grade).  
  
-   Erro  
  
-   Desempenho crítico (somente[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Mesclagem de execução longa (somente[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Expirando em breve/Expirado (somente[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Assinatura não inicializada (somente[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Tentando novamente comando com falha  
  
-   Sincronizando  
  
-   Não sincronizando  
  
 A ordem de classificação também determina qual valor será exibido se uma determinada assinatura estiver em mais de um estado. Por exemplo, se uma assinatura tiver um erro e expirar em breve, a coluna **Status** exibirá **Erro**.  
  
 Os valores de status **Desempenho crítico**, **Mesclagem de execução longa**, **Expirando em breve/Expirado**e **Assinatura não inicializada** são avisos. Quando um aviso é exibido, a coluna **Status** também exibe se um agente está sincronizando. Por exemplo, o status poderia ser **Sincronizando, Desempenho Crítico**.  
  
 Os valores de status **Expirando em breve/Expirado** e **Mesclagem de Execução Longa** só poderão ser exibidos se os limites forem definidos. O valor de status **Desempenho crítico** só pode ser exibido depois de cinco sincronizações de assinatura com o mesmo tipo de conexão (discada ou LAN). Para obter informações sobre medidas de desempenho e definir limites, consulte [Monitor Performance with Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) (Monitorar o desempenho com o Replication Monitor) e [Set Thresholds and Warnings in Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) (Definir limites e avisos no Replication Monitor).  
  
 **Assinatura**  
 O nome de cada assinatura no formato:*SubscriberName: SubscriptionDatabaseName*.  
  
 **Nome amigável**  
 Somente o[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A descrição de cada assinatura. A descrição é inserida na caixa de diálogo **Propriedades da assinatura** ou especificada com o parâmetro **@description** de [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) ou [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Os usuários geralmente usam a descrição como um "nome amigável" ou apelido para a assinatura.  
  
 **Desempenho**  
 Somente o[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A classificação de desempenho de cada assinatura, com base nas medidas mais recentes de taxa de entrega calculadas pelo Replication Monitor. A classificação é determinada comparando o desempenho de uma assinatura individual com o desempenho histórico médio de assinaturas com a publicação que tem o mesmo tipo de conexão (discada ou LAN). O Replication Monitor exibe um valor após a ocorrência de cinco sincronizações com 50 ou mais alterações cada, no mesmo tipo de conexão. Se houver menos de cinco sincronizações com 50 ou mais alterações ou se a sincronização mais recente tiver menos de 50 alterações, essa coluna ficará em branco.  
  
> [!NOTE]  
>  O desempenho é baseado no tipo de conexão exibido na coluna **Conexão** ; portanto, é possível que uma assinatura com uma taxa de entrega mais baixa exiba uma classificação de desempenho melhor do que outra assinatura, se a primeira assinatura estiver sincronizada em uma conexão mais lenta.  
  
 A classificação de desempenho é um dos seguintes valores:  
  
-   Excelente  
  
-   Bom  
  
-   Razoável  
  
-   Fraco  
  
 Para obter mais informações sobre como as classificações de desempenho são definidas e como os limites de desempenho são configurados, consulte [Monitor Performance with Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) (Monitorar o desempenho com o Replication Monitor).  
  
 **Taxa de Entrega**  
 O número de linhas por segundo processado pelo Merge Agent.  
  
 **Última Sincronização**  
 A hora da última execução do Merge Agent. As alterações podem ou não ter sido processadas durante essa sincronização. Se a sincronização estiver em progresso, um valor da porcentagem concluída será exibido.  
  
 **Duration**  
 A quantidade de tempo de execução do Merge Agent durante a última sincronização. O tempo representa o tempo decorrido, se o Merge Agent estiver sendo executado no momento, e o tempo total, se o Merge Agent foi sincronizado anteriormente.  
  
 **Conexão**  
 Somente o[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. O tipo de conexão entre o Assinante e o Editor. Os valores possíveis são **LAN**, **Discada**e **Internet**. O valor **Internet** será exibido se a assinatura usar sincronização da Web.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e realizar tarefas para uma assinatura &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Exibir informações e realizar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Sincronização da Web para replicação de mesclagem](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
