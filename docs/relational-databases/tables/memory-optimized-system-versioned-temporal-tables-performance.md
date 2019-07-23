---
title: Desempenho de tabelas temporais com controle de versão do sistema e otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 2e110984-7703-4806-a24b-b41e8c3018c6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01db1809ae4a16183673291c135e178dfac5cd7d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139627"
---
# <a name="memory-optimized-system-versioned-temporal-tables-performance"></a>Desempenho de tabelas temporais com controle de versão do sistema e otimização de memória

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Este tópico aborda algumas considerações de desempenho específicas ao usar tabelas temporais com versão do sistema e otimização de memória.

- Quando você adiciona controle de versão a uma tabela não temporal existente, espera impacto de desempenho nas operações de atualização e exclusão porque a tabela de histórico é atualizada automaticamente.
- Cada atualização e exclusão é registrada na tabela de histórico otimizada na memória interna, portanto você pode experimentar consumo de memória inesperado se sua carga de trabalho usar muito essas duas operações. Portanto, aconselhamos que você faça o seguinte:

  - Não execute grandes exclusões da tabela atual para aumentar a RAM disponível limpando o espaço. Considere a exclusão de dados em vários lotes com fluxos de dados invocados manualmente entre eles invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)ou enquanto **SYSTEM_VERSIONING = OFF**.
  - Não execute grandes atualizações de tabela de uma só vez, pois isso pode resultar em consumo de memória duas vezes maior que a quantidade de memória necessária para atualizar uma tabela de otimização de memória não temporal. O consumo duplicado de memória é temporário, pois a tarefa de liberação de dados funciona regularmente para manter o consumo de memória da tabela de preparo interna dentro dos limites projetados no estado estável (cerca de 10% do consumo de memória da tabela temporal atual). Considere a possibilidade de fazer atualizações grandes em vários lotes ou durante **SYSTEM_VERSIONING = OFF**, por exemplo, usando atualizações para definir os padrões de colunas recém-adicionadas.

- O período de ativação para a tarefa de fluxo de dados não é configurável, mas você pode impor o processo invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md).
- Considere usar columnstore clusterizado como uma opção de armazenamento de tabela de histórico com base em disco, especialmente se você planeja executar análise de consultas em dados históricos que usam funções de agregação ou janelas. Nesse caso, columnstore clusterizado será uma opção ideal para a tabela de histórico, uma vez que oferece compactação de dados e o comportamento "inserção amigável" que está de acordo com a forma pela qual os dados de histórico estão senso gerados.

## <a name="see-also"></a>Consulte Também

- [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Criação de uma tabela temporal com controle da versão do sistema e otimização de memória](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)
- [Trabalhando com tabelas temporais com controle da versão do sistema e otimização de memória](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [Monitorando tabelas temporais com controle da versão do sistema e otimização de memória](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
