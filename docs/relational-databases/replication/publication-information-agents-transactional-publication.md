---
title: Agentes (Transacional – SSMS)
description: Descreve a guia "Agentes" da publicação transacional selecionada no SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: ae95cc4fd67b7843d773a2dc175dd89f1784025b
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321373"
---
# <a name="publication-information-agents-transactional-publication"></a>Informações da Publicação, Agentes (publicação transacional)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  A guia **Agentes** exibe informações resumidas sobre os agentes para a publicação selecionada. Informações sobre o Snapshot Agent e Log Reader Agent são exibida para todas as publicações transacionais. Informações sobre o Queue Reader Agent são exibidas para essas publicações transacionais que estão habilitadas para assinaturas de atualização enfileirada.  
  
## <a name="options"></a>Opções  
 Para obter informações mais detalhadas e tarefas relacionadas a um agente, clique com o botão direito do mouse na linha desse agente e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas**.  
  
-   **Escolher Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas**.  
  
-   **Filtro**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro**.  
  
-   **Limpar Filtro**: Limpe todas as configurações de filtro para a grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Status**  
 O status de cada agente de replicação associado à publicação. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Tentando novamente comandos com falha  
  
-   Não está sendo executado  
  
-   Executando  
  
-   Concluído  
  
 **Agente**  
 O nome de cada agente de replicação associado à publicação. O Distribution Agent é associado com assinaturas para essa publicação. Para obter mais informações, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Última Hora de Início**  
 A última vez que o agente foi iniciado.  
  
 **Duration**  
 O tempo durante o qual o agente foi executado. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication.md)  
 [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
  
