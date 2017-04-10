---
title: "Informa&#231;&#245;es da Publica&#231;&#227;o, Todas as Assinaturas (publica&#231;&#227;o de instant&#226;neo) | Microsoft Docs"
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
  - "sql13.rep.monitor.publicationinfo.allsubscriptions.snapshot.f1"
ms.assetid: 7ce656c2-6e60-4625-8955-1daff641070c
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Informa&#231;&#245;es da Publica&#231;&#227;o, Todas as Assinaturas (publica&#231;&#227;o de instant&#226;neo)
  A guia **Todas as Assinaturas** exibe informações sobre todas as assinaturas na publicação de instantâneo selecionada.  
  
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
 O status de cada assinatura, que é determinado pelo status do Snapshot Agent ou do Distribution Agent (o status com prioridade mais alta é exibido).  
  
 Por padrão, a grade que contém informações de assinatura é classificada pela coluna **Status** . A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, os erros são sempre mostrados na parte superior da grade).  
  
-   Erro  
  
-   Expirando em breve/Expirado (somente [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Assinatura não inicializada (somente [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores)  
  
-   Tentando novamente comando com falha  
  
-   Sincronizando  
  
-   Não sincronizando  
  
 A ordem de classificação também determina qual valor será exibido se uma determinada assinatura estiver em mais de um estado. Por exemplo, se uma assinatura tiver um erro e expirar em breve, a coluna **Status** exibirá **Erro**.  
  
 Os valores de status **expirando em breve/expirado** e **assinatura não inicializada** são avisos. Quando um aviso for exibido, a coluna **Status** também será exibida se um agente estiver em execução. Por exemplo, o status poderia ser **executando, expirando em breve/expirado**.  
  
 O valor de status **expirando em breve/expirado** será exibida somente se for definido um limite. Para obter informações sobre como definir limites, consulte [definir limites e avisos no Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Assinatura**  
 O nome de cada assinatura, no formato: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Última Sincronização**  
 A hora da última execução do Distribution Agent. Se a sincronização estiver em andamento, **Em andamento** será exibido.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  