---
title: Novo perfil de agente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8549be8d4c8a40aaaa35c171e0d2183c7b490768
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007284"
---
# <a name="new-agent-profile"></a>Novo Perfil de Agente
  Use a caixa de diálogo **Novo Perfil de Agente** para criar um novo perfil. Novos perfis sempre são baseados em perfis existentes, mas eles podem ser modificados para atender aos requisitos do aplicativo. Depois que um perfil é criado ele pode ser aplicado a trabalhos de agentes futuros e existentes na caixa de diálogo **Perfis de Agente** . Os valores de parâmetro de agente podem ser editados na caixa de diálogo \<**AgentProfileName> Propriedades**.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Insira um nome para o perfil.  
  
 **Descrição**  
 Insira uma descrição para o perfil.  
  
 **Parâmetro**  
 Os parâmetros de agente incluídos no perfil. O perfil no qual o perfil novo é baseado não especifica necessariamente um valor para cada parâmetro. Para consultar todos os parâmetros válidos de um determinado agente, desmarque a caixa de seleção **Mostrar apenas os parâmetros usados neste perfil** . Para obter descrições de cada parâmetro, consulte.  
  
-   [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
-   [Agente do Leitor de Log de Replicação](agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](agents/replication-distribution-agent.md)  
  
-   [Agente de Mesclagem de Replicação](agents/replication-merge-agent.md)  
  
-   [Agente de Leitor de Fila de Replicação](agents/replication-queue-reader-agent.md)  
  
 **Valor padrão**  
 O valor padrão para cada parâmetro de agente.  
  
 **Value**  
 O valor especificado para o parâmetro no perfil no qual o perfil novo é baseado. Edite esse campo para obter qualquer valor de parâmetro que você queira alterar.  
  
 **Mostrar apenas os parâmetros usados neste perfil**  
 Desmarque para mostrar todos os parâmetros válidos para um determinado agente.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com perfis do Agente de Replicação](agents/work-with-replication-agent-profiles.md)   
 [Visão geral dos agentes de replicação](agents/replication-agents-overview.md)   
 [Perfis do agente de replicação](agents/replication-agent-profiles.md)  
  
  