---
title: "MSSQL_REPL027056 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_REPL027056"
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_REPL027056
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|27056|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O processo de mesclagem não pôde alterar o histórico de geração no '%1'. Ao solucionar o problema, reinicie a sincronização com o log de histórico detalhado e especifique um arquivo de saída no qual será realizada a gravação.|  
  
## Explicação  
 Geralmente, esse erro é gerado como resultado da contenção em tabelas do sistema de replicação de mesclagem que cresceram exageradamente. As tabelas grandes do sistema são normalmente causadas por um longo período de retenção de publicação, pois os metadados devem ser armazenados nessas tabelas até que o período de retenção seja atingido.  
  
## Ação do usuário  
 **Para resolver o problema:**  
  
1.  Diminua o valor de-**DownloadGenerationsPerBatch** e **- UploadGenerationsPerBatch** parâmetros para o Merge Agent permitir que o processamento continue enquanto você aborda subjacente emitem causando o erro. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do agente de replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros de Prompt de comando do agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Conceitos de executáveis do agente de replicação](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Especifique a menor definição possível para o período de retenção de publicação. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
3.  Como parte da manutenção de replicação de mesclagem, verifique periodicamente o crescimento das tabelas do sistema associados com a replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory**, e **MSmerge_tombstone**, **MSmerge_current_partition_mappings**, e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, consulte [reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  