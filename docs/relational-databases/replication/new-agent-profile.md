---
title: Novo perfil de agente | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 24a997bb8d14b331b8669fb2ce363b929a3279ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-agent-profile"></a>Novo Perfil de Agente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a caixa de diálogo **Novo Perfil de Agente** para criar um novo perfil. Novos perfis sempre são baseados em perfis existentes, mas eles podem ser modificados para atender aos requisitos do aplicativo. Depois que um perfil é criado ele pode ser aplicado a trabalhos de agentes futuros e existentes na caixa de diálogo **Perfis de Agente** . Os valores de parâmetro de agente podem ser editados na caixa de diálogo \<**AgentProfileName> Propriedades**.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Insira um nome para o perfil.  
  
 **Descrição**  
 Insira uma descrição para o perfil.  
  
 **Parâmetro**  
 Os parâmetros de agente incluídos no perfil. O perfil no qual o perfil novo é baseado não especifica necessariamente um valor para cada parâmetro. Para consultar todos os parâmetros válidos de um determinado agente, desmarque a caixa de seleção **Mostrar apenas os parâmetros usados neste perfil** . Para obter descrições de cada parâmetro, consulte.  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [Agente do Leitor de Log de Replicação](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Agente de Mesclagem de Replicação](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Agente de Leitor de Fila de Replicação](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **Valor padrão**  
 O valor padrão para cada parâmetro de agente.  
  
 **Value**  
 O valor especificado para o parâmetro no perfil no qual o perfil novo é baseado. Edite esse campo para obter qualquer valor de parâmetro que você queira alterar.  
  
 **Mostrar apenas os parâmetros usados neste perfil**  
 Desmarque para mostrar todos os parâmetros válidos para um determinado agente.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
