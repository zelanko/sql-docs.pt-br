---
description: Informações da Publicação, Agentes (publicação de mesclagem)
title: Informações da publicação, agentes (publicação de mesclagem) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.merge.f1
ms.assetid: 73ff590a-20da-4f10-b592-c60b7226d22b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce84b55a553b26e6fe9141601987f1e743584699
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88493872"
---
# <a name="publication-information-agents-merge-publication"></a>Informações da Publicação, Agentes (publicação de mesclagem)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  A guia **Agentes** exibe informações resumidas sobre o Snapshot Agent para a publicação selecionada.  
  
## <a name="options"></a>Opções  
 Para obter informações mais detalhadas e tarefas relacionadas ao Snapshot Agent, clique com o botão direito do mouse na linha do agente e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas** .  
  
-   **Selecionar Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas** .  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro** .  
  
-   **Limpar Filtro**: limpe as configurações de filtro da grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Status**  
 O status do Snapshot Agent. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Tentando novamente comandos com falha  
  
-   Não está sendo executado  
  
-   Concluído  
  
 **Agente**  
 O Snapshot Agent. Essa é a única publicação associada a uma publicação de mesclagem. O Merge Agent é associado a assinaturas para essa publicação. Para obter mais informações, confira [Exibir informações e executar tarefas com o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Última Hora de Início**  
 A última vez que o agente foi iniciado.  
  
 **Duration**  
 O tempo durante o qual o agente foi executado. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication.md)  
 [Exibir informações e executar tarefas com o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).
  
  
