---
title: "Informa&#231;&#245;es da Publica&#231;&#227;o, Todas as Assinaturas (publica&#231;&#227;o transacional) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.allsubscriptions.tran.f1"
ms.assetid: 7073350c-f667-4f70-88e9-152c9a1b08dd
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Informa&#231;&#245;es da Publica&#231;&#227;o, Todas as Assinaturas (publica&#231;&#227;o transacional)
  A guia **Todas as Assinaturas** exibe informações sobre todas as assinaturas na publicação transacional selecionada.  
  
## Opções  
 Para obter informações mais detalhadas e tarefas relacionadas a uma assinatura, clique com o botão direito do mouse na linha dessa assinatura e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas** .  
  
-   **Selecionar Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas** .  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro** .  
  
-   **Limpar Filtro**: limpe as configurações de filtro da grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Mostrar**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Selecione os estados de assinatura a serem exibidos para o tipo de assinatura selecionado. Por exemplo, você pode optar por exibir somente as assinaturas que tiverem um erro.  
  
 **Status**  
 O status de cada assinatura, determinado pelo status do Distribution Agent ou do Log Reader Agent (o status com prioridade mais alta é exibido; o status também pode ser determinado pelo Queue Reader Agent, se assinaturas de atualização enfileiradas forem usadas).  
  
 Por padrão, a grade que contém informações de assinatura é classificada pelo **Status** coluna (e, em seguida, classificados pelo **desempenho** coluna para essas assinaturas com o mesmo status). A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, os erros são sempre mostrados na parte superior da grade).  
  
-   Erro  
  
-   Desempenho crítico (somente [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Expirando em breve/Expirado (somente [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Assinatura não inicializada (somente [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Tentando novamente comando com falha  
  
-   Não está em execução  
  
-   Executando  
  
 A ordem de classificação também determina qual valor será exibido se uma determinada assinatura estiver em mais de um estado. Por exemplo, se uma assinatura tiver um erro e expirar em breve, a coluna **Status** exibirá **Erro**.  
  
 Os valores de status **desempenho crítico**, **expirando em breve/expirado**, e **assinatura não inicializada** são avisos. Quando um aviso for exibido, a coluna **Status** também será exibida se um agente estiver em execução. Por exemplo, o status poderia ser **Executando, Desempenho crítico**.  
  
 Os valores de status **desempenho crítico** e **expirando em breve/expirado** são exibidos somente se os limites são definidos. Para obter informações sobre medidas de desempenho e definir limites, consulte [monitorar o desempenho com o Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) e [definir limites e avisos no Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Assinatura**  
 O nome de cada assinatura, no formato: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Desempenho**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A classificação de desempenho de cada assinatura é baseada nas medidas mais atuais, calculadas pelo Replication Monitor, e, não reflete desempenho histórico. O desempenho é avaliado para assinaturas de publicações que têm limites de desempenho definidos; se os limites de desempenho não forem definidos para uma publicação, essa coluna exibirá **Não habilitado**. A classificação de desempenho é um dos seguintes valores:  
  
-   Excelente  
  
-   Bom  
  
-   Razoável  
  
-   Fraco  
  
-   Crítico  
  
 Se o desempenho for crítico, **Desempenho Crítico** será exibido na coluna **Status** . Para obter mais informações sobre como as avaliações de desempenho são definidas e como os limites de desempenho são configurados, consulte [monitorar o desempenho com o Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Latência**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. É o período médio de tempo que decorre entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante. A latência exibida é baseada nas medidas mais recentes calculadas pelo Replication Monitor. Para obter mais informações sobre como medir latência, consulte [medidas latência e validar conexões para replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  