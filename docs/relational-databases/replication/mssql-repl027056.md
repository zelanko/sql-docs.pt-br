---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1423e3639f64a4d82cf89fb16d7b849e445b0ed0
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlrepl027056"></a>MSSQL_REPL027056
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|27056|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O processo de mesclagem não pôde alterar o histórico de geração no '%1'. Ao solucionar o problema, reinicie a sincronização com o log de histórico detalhado e especifique um arquivo de saída no qual será realizada a gravação.|  
  
## <a name="explanation"></a>Explicação  
 Geralmente, esse erro é gerado como resultado da contenção em tabelas do sistema de replicação de mesclagem que cresceram exageradamente. As tabelas grandes do sistema são normalmente causadas por um longo período de retenção de publicação, pois os metadados devem ser armazenados nessas tabelas até que o período de retenção seja atingido.  
  
## <a name="user-action"></a>Ação do usuário  
 **Para resolver o problema:**  
  
1.  Diminua o valor dos parâmetros -**DownloadGenerationsPerBatch** e **- UploadGenerationsPerBatch** para o Merge Agent permitir que o processamento continue enquanto você aborda o problema subjacente que está causando o erro. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Especifique a menor definição possível para o período de retenção de publicação. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
3.  Como parte da manutenção da replicação de mesclagem, verifique esporadicamente o crescimento das tabelas do sistema associadas à replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory**, **MSmerge_tombstone**, **MSmerge_current_partition_mappings**e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

