---
title: sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
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
ms.openlocfilehash: 851c138e00300a303b1618041a16e2c38516968e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301206"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Possui informações sobre todas as solicitações atualmente ou recentemente ativas em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Ele lista uma linha por solicitação/consulta.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Chave para essa visão. ID numérico único associado à solicitação.|Único em todas as solicitações do sistema.|  
|session_id|**nvarchar(32)**|ID numérico único associado à sessão em que esta consulta foi executada. Consulte [sys.dm_pdw_exec_sessions &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Situação atual da solicitação.|'Correndo', 'Suspenso', 'Concluído', 'Cancelado', 'Falhou'.|  
|submit_time|**datetime**|Tempo em que o pedido foi submetido à execução.|**Data válida menor** ou igual à hora e start_time atuais.|  
|start_time|**datetime**|Tempo em que a execução do pedido foi iniciada.|NULL para solicitações enfileiradas; caso contrário, **data-hora** válida menor ou igual ao tempo atual.|  
|end_compile_time|**datetime**|Tempo em que o motor completou compilando a solicitação.|NULL para pedidos que ainda não foram compilados; caso contrário, uma **data válida menor** que start_time e menor ou igual ao tempo atual.|
|end_time|**datetime**|Tempo em que a execução do pedido foi concluída, falhou ou foi cancelada.|Nulo para solicitações enfileiradas ou ativas; caso contrário, uma **data-hora** válida menor ou igual à hora atual.|  
|total_elapsed_time|**int**|O tempo decorrido na execução desde que o pedido foi iniciado, em milissegundos.|Entre 0 e a diferença entre start_time e end_time.</br></br> Se total_elapsed_time exceder o valor máximo para um inteiro, total_elapsed_time continuará sendo o valor máximo. Esta condição gerará o aviso "O valor máximo foi excedido".</br></br> O valor máximo em milissegundos é o mesmo que 24,8 dias.|  
|label|**nvarchar (255)**|String de rótulo opcional associada a algumas instruções de consulta SELECT.|Qualquer string contendo 'a-z', 'A-Z', '0-9', ''_'.|  
|error_id|**nvarchar(36)**|ID único do erro associado à solicitação, se houver.|Ver [sys.dm_pdw_errors &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); definido como NULO se não ocorreu nenhum erro.|  
|database_id|**int**|Identificador de banco de dados usado por contexto explícito (por exemplo, USE DB_X).|Consulte ID em [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|command|**nvarchar(4000)**|Mantém o texto completo da solicitação conforme enviado pelo usuário.|Qualquer consulta válida ou texto de solicitação. Consultas com mais de 4000 bytes são truncadas.|  
|resource_class|**nvarchar(20)**|O grupo de carga de trabalho utilizado para esta solicitação. |Classes de recurso estáticas</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Classes de recurso dinâmicas</br>SmallRC</br>MediumRC</br>GrandeRC</br>XLargeRC|
|importance|**nvarchar(128)**|A importância de definir a solicitação executada em.  Esta é a importância relativa de uma solicitação neste grupo de carga de trabalho e em grupos de carga de trabalho para recursos compartilhados.  A importância especificada no classificador substitui a configuração de importância do grupo de carga de trabalho.</br>Aplica-se a: SQL Data Warehouse do Azure|NULO</br>low</br>below_normal</br>normal (padrão)</br>above_normal</br>high|
|group_name|**sysname** |Para solicitações que utilizam recursos, group_name é o nome do grupo de carga de trabalho em que a solicitação está sendo realizada.  Se a solicitação não utilizar recursos, group_name é nula.</br>Aplica-se a: SQL Data Warehouse do Azure|
|classifier_name|**sysname**|Para solicitações utilizando recursos, o nome do classificador usado para atribuir recursos e importância.||
|resource_allocation_percentage|**decimal (5,2)**|A quantidade percentual de recursos alocados para a solicitação.</br>Aplica-se a: SQL Data Warehouse do Azure|
|result_cache_hit|**Hexadecimal**|Detalhes se uma consulta concluída usou cache conjunto de resultados.  </br>Aplica-se a: SQL Data Warehouse do Azure| 1 = Impacto de cache do conjunto de resultados </br> 0 = Falha de cache do conjunto de resultados </br> Valores negativos = Razões pelas quais o cache de conjunto de resultados não foi utilizado.  Consulte a seção de observações para obter detalhes.|
||||
  
## <a name="remarks"></a>Comentários 
 Para obter informações sobre as linhas máximas retidas por essa exibição, consulte a seção Metadados no tópico [Limites de Capacidade.](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)

 O result_cache_hit é uma máscara de bitmask do uso de cache de conjunto de resultados de uma consulta.  Esta coluna pode ser a [| (Bitwise OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md) produto de um ou mais desses valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Impacto de cache do conjunto de resultados|  
|-**0x00**|Falha de cache do conjunto de resultados|  
|-**0x01**|O cache definido por resultados está desativado no banco de dados.|  
|-**0x02**|O cache definido por resultados está desativado na sessão. | 
|-**0x04**|O cache de conjunto de resultados está desativado devido a nenhuma fonte de dados para a consulta.|  
|-**0x08**|O cache definido por resultados está desativado devido aos predicados de segurança de nível de linha.|  
|-**0x10**|O cache definido por resultados está desativado devido ao uso de tabela do sistema, tabela temporária ou tabela externa na consulta.|  
|-**0x20**|O cache definido por resultados é desativado porque a consulta contém constantes de tempo de execução, funções definidas pelo usuário ou funções não determinísticas.|  
|-**0x40**|O cache definido pelo resultado é desativado devido ao tamanho estimado do conjunto de resultados ser muito grande (> 1 milhão de linhas).|  
|-**0x80**|O cache do conjunto de resultados está desativado porque o conjunto de resultados contém linhas com grande tamanho (>64kb).|  
  
## <a name="permissions"></a>Permissões

 Requer a permissão VIEW SERVER STAT.  
  
## <a name="security"></a>Segurança

 sys.dm_pdw_exec_requests não filtra os resultados da consulta de acordo com permissões específicas do banco de dados. Logins com permissão DO VIEW SERVER STATE podem obter resultados de consulta de resultados para todos os bancos de dados  
  
>[!WARNING]  
>Um invasor pode usar sys.dm_pdw_exec_requests para recuperar informações sobre objetos de banco de dados específicos simplesmente tendo permissão do ESTADO DO SERVIDOR VIEW e não tendo permissão específica do banco de dados.  
  
## <a name="see-also"></a>Consulte Também

 [SQL Data Warehouse e Dados Warehouse Paralelos Visão Dinâmica de Gerenciamento &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
