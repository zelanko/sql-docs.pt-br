---
title: "MSSQL_REPL027183 | Microsoft Docs"
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
  - "erro MSSQL_REPL027183"
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_REPL027183
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|27183|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O processo de mesclagem não pôde enumerar as alterações nos artigos que apresentaram filtros de linha com parâmetros. Se a falha persistir, aumente o tempo limite da consulta nesse processo, reduza o período de retenção da publicação e aprimore os índices nas tabelas publicadas.|  
  
## Explicação  
 Esse erro surge quando o tempo limite do Merge Agent ocorre durante o processamento de alterações em uma publicação filtrada. O tempo limite pode ser causado por um dos seguintes problemas:  
  
-   A otimização das partições pré-computadas não está sendo usada.  
  
-   Fragmentação de índice em colunas usadas para filtragem.  
  
-   Tabelas de metadados de mesclagem grandes, como **MSmerge_tombstone**, **MSmerge_contents**, e **MSmerge_genhistory**.  
  
-   Tabelas filtradas não associadas em uma chave exclusiva e associação de filtros que envolvem um grande número de tabelas.  
  
## Ação do usuário  
 Para resolver o problema:  
  
-   Aumente o valor da **- QueryTimeOut** problemas de parâmetro para o Merge Agent permitir que o processamento continue enquanto você aborda subjacente que está causando o erro. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do agente de replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros de Prompt de comando do agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Conceitos de executáveis do agente de replicação](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Use a otimização de partições pré-computadas, se possível. Por padrão, essa otimização será usada se um número de requisitos de publicação forem atendidos. Para obter mais informações sobre esses requisitos, consulte [otimizar desempenho de filtro parametrizado com partições pré-calculadas](../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). Se a publicação não satisfizer esses requisitos, considere reprojetar a publicação.  
  
-   Especifique a menor definição possível para o período de retenção da publicação, porque a replicação não poderá limpar os metadados nos bancos de dados de assinatura e publicação antes do período de retenção ser atingido. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Como parte da manutenção de replicação de mesclagem, verifique periodicamente o crescimento das tabelas do sistema associados com a replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory**, e **MSmerge_tombstone**, **MSmerge_current_partition_mappings**, e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, consulte [reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Certifique-se de que as colunas usadas para filtragem estejam indexadas corretamente e reconstrua tais índices, se necessário. Para obter mais informações, consulte [reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Definir o **join_unique_key** propriedade para filtros de junção que são baseados em colunas exclusivas. Para obter mais informações, consulte [Join Filters](../../relational-databases/replication/merge/join-filters.md).  
  
-   Limite o número de tabelas na hierarquia de filtro de junção. Se você estiver gerando filtros de junção de cinco ou mais tabelas, considere outras soluções: não filtre tabelas pequenas, que não estão sujeitas a alterações ou que sejam basicamente tabelas de pesquisa. Use filtros de junção somente entre tabelas que devem ser particionadas entre assinaturas.  
  
-   Faça um número menor de alterações em tabelas filtradas entre as sincronizações ou execute o Merge Agent mais frequentemente. Para obter mais informações sobre como definir agendas de sincronização, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  