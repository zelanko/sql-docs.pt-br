---
title: Desempenho de tabelas temporais com controle de versão do sistema e otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2e110984-7703-4806-a24b-b41e8c3018c6
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 96897ca8889af1c227e6304a358d0ab2b8154e72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="memory-optimized-system-versioned-temporal-tables-performance"></a>Desempenho de tabelas temporais com controle de versão do sistema e otimização de memória
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico aborda algumas considerações de desempenho específicas ao usar tabelas temporais com versão do sistema e otimização de memória.  
  
-   Quando você adiciona controle de versão a uma tabela não temporal existente, espera impacto de desempenho nas operações de atualização e exclusão porque a tabela de histórico é atualizada automaticamente.  
  
-   Cada atualização e exclusão é registrada na tabela de histórico otimizada na memória interna, portanto você pode experimentar consumo de memória inesperado se sua carga de trabalho usar muito essas duas operações. Portanto, aconselhamos que você faça o seguinte:  
  
    -   Não execute grandes exclusões da tabela atual para aumentar a RAM disponível limpando o espaço. Considere a exclusão de dados em vários lotes com fluxos de dados invocados manualmente entre eles invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)ou enquanto **SYSTEM_VERSIONING = OFF**.  
  
    -   Não execute grandes atualizações de tabela de uma vez pois isso pode resultar em consumo de memória que é duas vezes a quantidade de memória necessária para atualizar uma tabela de otimização de memória não temporal. Consumo de memória duplicado é temporário, pois a tarefa de fluxo de dados funciona regularmente para manter o consumo de memória da tabela interna de preparo dentro dos limites projetados no estado estável (aproximadamente 10% do consumo de memória de tabela de tempo atual). Considere a possibilidade de fazer atualizações grandes em vários lotes ou durante **SYSTEM_VERSIONING = OFF**, como usando atualizações para definir os padrões de colunas recém-adicionadas.  
  
-   O período de ativação para a tarefa de fluxo de dados não é configurável, mas você pode impor o processo invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md).  
  
-   Considere usar columnstore clusterizado como uma opção de armazenamento de tabela de histórico com base em disco, especialmente se você planeja executar análise de consultas em dados históricos que usam funções de agregação ou janelas. Nesse caso, columnstore clusterizado será uma opção ideal para a tabela de histórico, uma vez que oferece compactação de dados e o comportamento "inserção amigável" que está de acordo com a forma pela qual os dados de histórico estão senso gerados.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Criação de uma tabela temporal com controle da versão do sistema com otimização de memória](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [Trabalho com tabelas temporais com controle da versão do sistema com otimização de memória](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [Monitorando tabelas temporais com controle da versão do sistema com otimização de memória](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
