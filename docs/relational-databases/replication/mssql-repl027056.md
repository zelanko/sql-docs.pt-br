---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 20586254516f97552f3dbc181bc482f24a683d00
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764840"
---
# <a name="mssqlrepl027056"></a>MSSQL_REPL027056
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
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
  
3.  Como parte da manutenção para replicação de mesclagem, verifique ocasionalmente o crescimento das tabelas do sistema associado à replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory** e **MSmerge_tombstone**, **MSmerge_current_partition_mappings** e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
