---
description: sys.dm_exec_query_optimizer_info (Transact-SQL)
title: sys. dm_exec_query_optimizer_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_info_TSQL
- dm_exec_query_optimizer_info
- sys.dm_exec_query_optimizer_info_TSQL
- sys.dm_exec_query_optimizer_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_info dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9678d237863801b4ecad49167d1930a694859bae
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546590"
---
# <a name="sysdm_exec_query_optimizer_info-transact-sql"></a>sys.dm_exec_query_optimizer_info (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna estatísticas detalhadas sobre a operação do otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar esta exibição ao ajustar uma carga de trabalho para identificar problemas ou melhorias na otimização de consulta. Por exemplo, você pode usar o número total de otimizações, o valor de tempo decorrido e o valor de custo final para comparar as otimizações de consulta da carga de trabalho atual e quaisquer mudanças observadas durante o processo de ajuste. Alguns contadores fornecem dados que são relevantes apenas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uso de diagnóstico interno. Esses contadores são marcados como "Somente interno”.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_exec_query_optimizer_info**.  
  
|Name|Tipo de dados|Descrição|  
|----------|---------------|-----------------|  
|**neutraliza**|**nvarchar(4000)**|Nome do evento de estatísticas do otimizador.|  
|**occurrence**|**bigint**|Número de ocorrências do evento de otimização para este contador.|  
|**value**|**float**|Valor de propriedade médio por ocorrência de evento.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o  **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
    
## <a name="remarks"></a>Comentários  
 **Sys. dm_exec_query_optimizer_info** contém as seguintes propriedades (contadores). Todos os valores de ocorrência são cumulativos, e são definidos em 0 na reinicialização de sistema. Todos os valores dos campos de valores são definidos em NULL, na reinicialização de sistema. Todos os valores da coluna de valor especificam um uso médio do valor de ocorrência da mesma linha como o denominador no cálculo da média. Todas as otimizações de consulta são medidas quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o determina alterações no **dm_exec_query_optimizer_info**, incluindo consultas geradas pelo usuário e pelo sistema. A execução de um plano já armazenado em cache não altera valores em **dm_exec_query_optimizer_info**, somente otimizações são significativas.  
  
|Contador|Ocorrência|Valor|  
|-------------|----------------|-----------|  
|otimizações|Número total de otimizações.|Não aplicável|  
|tempo decorrido|Número total de otimizações.|Tempo médio decorrido por otimização de uma instrução individual (consulta), em segundos.|  
|custo final|Número total de otimizações.|Custo estimado médio para um plano otimizado em unidades de custo interno.|  
|plano trivial|Somente interno|Somente interno|  
|tarefas|Somente interno|Somente interno|  
|nenhum plano|Somente interno|Somente interno|  
|pesquisar 0|Somente interno|Somente interno|  
|pesquisar 0 vez|Somente interno|Somente interno|  
|pesquisar 0 tarefa|Somente interno|Somente interno|  
|pesquisar 1|Somente interno|Somente interno|  
|pesquisar 1 vez|Somente interno|Somente interno|  
|pesquisar 1 tarefa|Somente interno|Somente interno|  
|pesquisa 2|Somente interno|Somente interno|  
|pesquisar 2 vezes|Somente interno|Somente interno|  
|pesquisar 2 tarefas|Somente interno|Somente interno|  
|estágio de ganho 0 para estágio 1|Somente interno|Somente interno|  
|estágio de ganho 1 para estágio 2|Somente interno|Somente interno|  
|tempo limite|Somente interno|Somente interno|  
|limite de memória excedido|Somente interno|Somente interno|  
|insert stmt|Número de otimizações existentes para instruções INSERT.|Não aplicável|  
|delete stmt|Número de otimizações existentes para instruções DELETE.|Não aplicável|  
|update stmt|Número de otimizações existentes para instruções UPDATE.|Não aplicável|  
|contém subconsulta|Número de otimizações para uma consulta que contém ao menos uma subconsulta.|Não aplicável|  
|unnest falhou|Somente interno|Somente interno|  
|tabelas|Número total de otimizações.|Calcule o número médio de tabelas referenciadas por consulta otimizada.|  
|dicas|Número de vezes que alguma dica foi especificada. Dicas contadas incluem: dicas de consulta JOIN, GROUP, UNION e FORCE ORDER, a opção definida FORCE PLAN e dicas de associação.|Não aplicável|  
|dica order|Número de vezes que dica de ordem de força foi especificada.|Não aplicável|  
|dica de associação|Número de vezes que o algoritmo de junção foi forçado por uma dica de associação.|Não aplicável|  
|exibir referência|Número de vezes que uma exibição foi referenciada em uma consulta.|Não aplicável|  
|consulta remota|Número de otimizações em que a consulta referencia ao menos uma fonte de dados remota, como uma tabela com um nome de quatro partes ou um resultado OPENROWSET.|Não aplicável|  
|DOP máximo|Número total de otimizações.|Valor efetivo médio MAXDOP para um plano otimizado. Por padrão, MAXDOP efetivo é determinado pela opção de configuração de servidor **grau máximo de paralelismo** e pode ser substituído por uma consulta específica pelo valor da dica de consulta MAXDOP.|  
|nível máximo de recursão|Número de otimizações em que um nível MAXRECURSION maior que 0 foi especificado com a dica de consulta.|Nível MAXRECURSION médio em otimizações onde um nível máximo de recursão especificado com a dica de consulta.|  
|exibições indexadas carregadas|Somente interno|Somente interno|  
|exibições indexadas correspondentes|Número de otimizações em que uma ou mais exibições indexadas foram correspondidas.|Número médio de exibições correspondentes.|  
|exibições indexadas usadas|Número de otimizações em que uma ou mais exibições indexadas são usadas no plano de saída depois de correspondidas.|Número médio de exibições usadas.|  
|exibições indexadas atualizadas|Número de otimizações de uma instrução DML que produzem um plano que mantém uma ou mais exibições indexadas.|Número médio de exibições mantidas.|  
|solicitação de cursor dinâmico|Número de otimizações em que uma solicitação de cursor dinâmico foi especificada.|Não aplicável|  
|solicitação de cursor de avanço rápido|Número de otimizações em que uma solicitação de cursor de avanço rápido foi especificada.|Não aplicável|  
|merge stmt|Número de otimizações existentes para instruções MERGE.|Não aplicável|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-viewing-statistics-on-optimizer-execution"></a>a. Exibindo estatísticas de execução do otimizador  
 Quais são as estatísticas de execução do otimizador atuais para esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]?  
  
```  
SELECT * FROM sys.dm_exec_query_optimizer_info;  
```  
  
### <a name="b-viewing-the-total-number-of-optimizations"></a>B. Exibindo o número total de otimizações  
 Quantas otimizações foram executadas?  
  
```  
SELECT occurrence AS Optimizations FROM sys.dm_exec_query_optimizer_info  
WHERE counter = 'optimizations';  
```  
  
### <a name="c-average-elapsed-time-per-optimization"></a>C. Tempo médio decorrido por otimização  
 Qual o tempo médio decorrido por otimização?  
  
```  
SELECT ISNULL(value,0.0) AS ElapsedTimePerOptimization  
FROM sys.dm_exec_query_optimizer_info WHERE counter = 'elapsed time';  
```  
  
### <a name="d-fraction-of-optimizations-that-involve-subqueries"></a>D. Fracionamento de otimizações que envolvem subconsultas  
 Que fração de consultas otimizadas continha uma subconsulta?  
  
```  
SELECT (SELECT CAST (occurrence AS float) FROM sys.dm_exec_query_optimizer_info WHERE counter = 'contains subquery') /  
       (SELECT CAST (occurrence AS float)   
        FROM sys.dm_exec_query_optimizer_info WHERE counter = 'optimizations')  
        AS ContainsSubqueryFraction;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


