---
title: sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 72af3975378b2450e51b3880e8814705bb514c1a
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811403"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as solicitações no momento ou recentemente [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]ativas no. Ele lista uma linha por solicitação/consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Chave para esta exibição. ID numérica exclusiva associada à solicitação.|Exclusivo em todas as solicitações no sistema.|  
|session_id|**nvarchar(32)**|ID numérica exclusiva associada à sessão na qual essa consulta foi executada. Consulte [Sys. dm _pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Status atual da solicitação.|' Running ', ' SUSPENDED ', ' Completed ', ' cancelado ', ' Failed '.|  
|submit_time|**datetime**|Hora em que a solicitação foi enviada para execução.|**DateTime** válido menor ou igual à hora atual e start_time.|  
|start_time|**datetime**|Hora em que a execução da solicitação foi iniciada.|NULL para solicitações em fila; caso contrário, **DateTime** válido menor ou igual à hora atual.|  
|end_compile_time|**datetime**|Hora em que o mecanismo concluiu a compilação da solicitação.|NULO para solicitações que ainda não foram compiladas; caso contrário, um **DateTime** válido menor que start_time e menor ou igual à hora atual.|
|end_time|**datetime**|Hora em que a execução da solicitação foi concluída, falhou ou foi cancelada.|NULL para solicitações em fila ou ativas; caso contrário, um **DateTime** válido menor ou igual à hora atual.|  
|total_elapsed_time|**int**|Tempo decorrido na execução desde que a solicitação foi iniciada, em milissegundos.|Entre 0 e a diferença entre start_time e end_time.</br></br> Se total_elapsed_time exceder o valor máximo de um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição irá gerar o aviso "o valor máximo foi excedido".</br></br> O valor máximo em milissegundos é o mesmo que 24,8 dias.|  
|chamada|**nvarchar(255)**|Cadeia de caracteres de rótulo opcional associada a algumas instruções de consulta SELECT.|Qualquer cadeia de caracteres contendo ' a-z ', ' A-Z ', ' 0-9 ', ' _ '.|  
|error_id|**nvarchar(36)**|ID exclusiva do erro associado à solicitação, se houver.|Consulte [Sys. dm _pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); Defina como NULL se nenhum erro tiver ocorrido.|  
|database_id|**int**|Identificador do banco de dados usado pelo contexto explícito (por exemplo, USE DB_X).|Consulte ID em [Sys. databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|command|**nvarchar(4000)**|Mantém o texto completo da solicitação como enviado pelo usuário.|Qualquer consulta ou texto de solicitação válido. Consultas com mais de 4000 bytes são truncadas.|  
|resource_class|**nvarchar(20)**|A classe de recurso para essa solicitação. Consulte **concurrency_slots_used** relacionados em [Sys. dm _PDW_RESOURCE_WAITS &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).  Para obter mais informações sobre classes de recursos, consulte [classes de recursos & gerenciamento de carga de trabalho](https://docs.microsoft.com/azure/sql-data-warehouse/resource-classes-for-workload-management) |Classes de recurso estáticas</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Classes de recurso dinâmicas</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(32)**|A configuração de importância à qual a solicitação foi enviada. As solicitações com uma prioridade mais baixa permanecerão enfileiradas no estado suspenso, se as solicitações de maior importância forem enviadas.  As solicitações com maior importância serão executadas antes das solicitações de importância inferior que foram enviadas anteriormente.  Para obter mais informações sobre importância, consulte [importância da carga de trabalho](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-importance).  |NULL</br>low</br>below_normal</br>normal (padrão)</br>above_normal</br>high|
|group_name| |Reservado para uso interno.</br>Aplica-se a: Azure SQL Data Warehouse|
|resource_allocation_percentage| |Reservado para uso interno.</br>Aplica-se a: Azure SQL Data Warehouse|
|result_set_cache|**bit**|Detalha se uma consulta concluída foi um problema de cache de resultado (1) ou não (0).|0,1|
||||
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte a seção de metadados no tópico [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .   
  
## <a name="permissions"></a>Permissões

 Requer a permissão VIEW SERVER STAT.  
  
## <a name="security"></a>Segurança

 sys. dm _pdw_exec_requests não filtra os resultados da consulta de acordo com as permissões específicas do banco de dados. Os logons com a permissão VIEW SERVER STATE podem obter resultados da consulta de resultados para todos os bancos de dados  
  
>[!WARNING]  
>Um invasor pode usar sys. dm _pdw_exec_requests para recuperar informações sobre objetos de banco de dados específicos, simplesmente tendo a permissão VIEW SERVER STATE e não tem uma permissão específica do banco de dados.  
  
## <a name="see-also"></a>Consulte também

 [Exibições &#40;de gerenciamento dinâmico SQL data warehouse e Parallel Data Warehouse TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md) 
