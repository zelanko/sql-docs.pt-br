---
description: MSSQL_REPL027183
title: MSSQL_REPL027183 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027183 error
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 123936b94066af78dce6cd9c2f8a4cdeec7f2fbd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475697"
---
# <a name="mssql_repl027183"></a>MSSQL_REPL027183
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|27183|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O processo de mesclagem não pôde enumerar as alterações nos artigos que apresentaram filtros de linha com parâmetros. Se a falha persistir, aumente o tempo limite da consulta nesse processo, reduza o período de retenção da publicação e aprimore os índices nas tabelas publicadas.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro surge quando o tempo limite do Merge Agent ocorre durante o processamento de alterações em uma publicação filtrada. O tempo limite pode ser causado por um dos seguintes problemas:  
  
-   A otimização das partições pré-computadas não está sendo usada.  
  
-   Fragmentação de índice em colunas usadas para filtragem.  
  
-   Tabelas de metadados de mesclagens grandes, como **MSmerge_tombstone**, **MSmerge_contents** e **MSmerge_genhistory**.  
  
-   Tabelas filtradas não associadas em uma chave exclusiva e associação de filtros que envolvem um grande número de tabelas.  
  
## <a name="user-action"></a>Ação do usuário  
 Como resolver o problema:  
  
-   Aumente o valor do parâmetro **-QueryTimeOut** do Agente de Mesclagem para permitir que o processamento continue enquanto você aborda os problemas subjacentes que estão provocando o erro. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Use a otimização de partições pré-computadas, se possível. Por padrão, essa otimização será usada se um número de requisitos de publicação forem atendidos. Para obter mais informações sobre esses requisitos, consulte [Otimizar o desempenho de filtro com parâmetros com partições pré-computadas](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md). Se a publicação não satisfizer esses requisitos, considere reprojetar a publicação.  
  
-   Especifique a menor definição possível para o período de retenção da publicação, porque a replicação não poderá limpar os metadados nos bancos de dados de assinatura e publicação antes do período de retenção ser atingido. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Como parte da manutenção da replicação de mesclagem, verifique esporadicamente o crescimento das tabelas do sistema associadas à replicação de mesclagem: **MSmerge_contents**, **MSmerge_genhistory**, **MSmerge_tombstone**, **MSmerge_current_partition_mappings** e **MSmerge_past_partition_mappings**. Periodicamente, indexe novamente essas tabelas. Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Certifique-se de que as colunas usadas para filtragem estejam indexadas corretamente e reconstrua tais índices, se necessário. Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Defina a propriedade **join_unique_key** para filtros de junção com base em colunas exclusivas. Para obter mais informações, consulte [Join Filters](../../relational-databases/replication/merge/join-filters.md).  
  
-   Limite o número de tabelas na hierarquia de filtro de junção. Se você estiver gerando filtros de junção de cinco ou mais tabelas, considere outras soluções: não filtre tabelas pequenas, que não estão sujeitas a alterações ou que sejam basicamente tabelas de pesquisa. Use filtros de junção somente entre tabelas que devem ser particionadas entre assinaturas.  
  
-   Faça um número menor de alterações em tabelas filtradas entre as sincronizações ou execute o Merge Agent mais frequentemente. Para obter mais informações sobre como definir agendas de sincronização, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
