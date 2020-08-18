---
description: MSSQL_ENG014151
title: MSSQL_ENG014151 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 5c0ebe75223445557b6a462c8dbd75391b41a857
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88326852"
---
# <a name="mssql_eng014151"></a>MSSQL_ENG014151
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14151|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Replicação-%s: falha no agente %s. %s|  
  
## <a name="explanation"></a>Explicação  
 Este erro ocorre para qualquer falha de agente de replicação. O texto ao término da mensagem depende do contexto da falha.  
  
## <a name="user-action"></a>Ação do usuário  
 Este erro pode acontecer em várias situações; use as seguintes abordagens, conforme necessário:  
  
-   Reinicie o agente com falha para verificar se será possível executá-lo sem falhas agora. Para obter mais informações, consulte [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Conceitos dos executáveis do agente de replicação](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Verifique o histórico de agente e o histórico de trabalho para outros erros que aconteceram quase no mesmo momento. Para obter informações sobre exibir detalhes de status e de erro do agente no Replication Monitor, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   Verifique se a conectividade básica está funcionado entre os computadores acessados pelo agente e, depois, conecte-se a cada computador com um utilitário como [sqlcmd Utility](../../tools/sqlcmd-utility.md). Ao se conectar, use a mesma conta com a qual o agente faz conexões. Para obter mais informações sobre as permissões exigidas para cada conta de agente, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Se o erro ocorrer ao criar ou aplicar um instantâneo, verifique os arquivos no diretório de instantâneos para erros. 
  
-   Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levaram ao erro e/ou as mensagens de erros adicionais.  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
