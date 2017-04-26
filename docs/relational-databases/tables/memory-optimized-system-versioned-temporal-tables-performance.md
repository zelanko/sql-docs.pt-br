---
title: "Desempenho de tabelas temporais com controle de versão do sistema e otimização de memória | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2e110984-7703-4806-a24b-b41e8c3018c6
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d67b2ac2eb3f10bd5ecbf973ec97d12566973738
ms.lasthandoff: 04/11/2017

---
# <a name="memory-optimized-system-versioned-temporal-tables-performance"></a>Desempenho de tabelas temporais com controle de versão do sistema e otimização de memória
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico aborda algumas considerações de desempenho específicas ao usar tabelas temporais com versão do sistema e otimização de memória.  
  
-   Quando você adiciona controle de versão a uma tabela não temporal existente, espera impacto de desempenho nas operações de atualização e exclusão porque a tabela de histórico é atualizada automaticamente.  
  
-   Cada atualização e exclusão é registrada na tabela de histórico otimizada na memória interna, portanto você pode experimentar consumo de memória inesperado se sua carga de trabalho usar muito essas duas operações. Portanto, aconselhamos que você faça o seguinte:  
  
    -   Não execute grandes exclusões da tabela atual para aumentar a RAM disponível limpando o espaço. Considere a exclusão de dados em vários lotes com fluxos de dados invocados manualmente entre eles invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)ou enquanto **SYSTEM_VERSIONING = OFF**.  
  
    -   Não execute grandes atualizações de tabela de uma vez pois isso pode resultar em consumo de memória que é duas vezes a quantidade de memória necessária para atualizar uma tabela de otimização de memória não temporal. Consumo de memória duplicado é temporário, pois a tarefa de fluxo de dados funciona regularmente para manter o consumo de memória da tabela interna de preparo dentro dos limites projetados no estado estável (aproximadamente 10% do consumo de memória de tabela de tempo atual). Considere a possibilidade de fazer atualizações grandes em vários lotes ou durante **SYSTEM_VERSIONING = OFF**, como usando atualizações para definir os padrões de colunas recém-adicionadas.  
  
-   O período de ativação para a tarefa de fluxo de dados não é configurável, mas você pode impor o processo invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md).  
  
-   Considere usar columnstore clusterizado como uma opção de armazenamento de tabela de histórico com base em disco, especialmente se você planeja executar análise de consultas em dados históricos que usam funções de agregação ou janelas. Nesse caso, columnstore clusterizado será uma opção ideal para a tabela de histórico, uma vez que oferece compactação de dados e o comportamento "inserção amigável" que está de acordo com a forma pela qual os dados de histórico estão senso gerados.  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Performance%20Considerations%20with%20Memory-Optimized%20System-Versioned%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Criação de uma tabela temporal com controle da versão do sistema com otimização de memória](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [Trabalho com tabelas temporais com controle da versão do sistema com otimização de memória](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [Monitorando tabelas temporais com controle da versão do sistema com otimização de memória](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

