---
title: MSSQL_ENG014150 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014150 error
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07fcbe83f92a523eea000a9a63b4a72a991228fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233046"
---
# <a name="mssqleng014150"></a>MSSQL_ENG014150
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14150|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Replicação-%s: agente %s bem-sucedida. %s|  
  
## <a name="explanation"></a>Explicação  
 Essa mensagem indica que um agente de replicação concluiu a execução com êxito. A replicação usa os seguintes agentes:  
  
-   O Snapshot Agent. Esse agente é usado por todas as publicações.  
  
-   O Log Reader Agent. Esse agente é usado por todas as publicações transacionais.  
  
-   O Queue Reader Agent. Esse agente é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
-   O Distribution Agent. Esse agente sincroniza as assinaturas para publicações transacionais e de instantâneo.  
  
-   O Merge Agent. Esse agente sincroniza as assinaturas para publicações de mesclagem.  
  
-   Trabalhos de manutenção de replicação.  
  
## <a name="user-action"></a>Ação do usuário  
 O Log Reader Agent, o Queue Reader Agent e o Distribution Agent são, em geral, executados continuamente, diferente de outros agentes, que são, em geral, executados sob demanda ou de forma programada. Se você não esperar que um agente tenha concluído a sua execução, verifique o estado do agente. Para obter mais informações, consulte [Monitor Replication Agents](agents/replication-agents.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administração do agente de replicação](agents/replication-agent-administration.md)   
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)   
 [Agente de Distribuição de Replicação](agents/replication-distribution-agent.md)   
 [Agente do Leitor de Log de Replicação](agents/replication-log-reader-agent.md)   
 [Agente de Mesclagem de Replicação](agents/replication-merge-agent.md)   
 [Agente de Leitor de Fila de Replicação](agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
  
