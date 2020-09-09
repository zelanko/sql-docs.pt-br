---
description: sp_check_dynamic_filters (Transact-SQL)
title: sp_check_dynamic_filters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 323740799308f19a15dd4c8ccede8bcfe106465f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539090"
---
# <a name="sp_check_dynamic_filters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Exibe informações sobre propriedades de filtro de linhas com parâmetros para uma publicação, em específico as funções usadas para gerar uma partição de dados filtrados para uma publicação e se a publicação está qualificada para usar partições pré-computadas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|É se a publicação é qualificada para usar partições preputadas; em que **1** significa que as partições já computadas podem ser usadas, e **0** significa que elas não podem ser usadas.|  
|**has_dynamic_filters**|**bit**|É se pelo menos um filtro de linha com parâmetros tiver sido definido na publicação; em que **1** significa que um ou mais filtros de linha com parâmetros existem e **0** significa que não existem filtros dinâmicos.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|Lista de funções usada para filtrar artigos em uma publicação, onde cada função está separada por um ponto-e-vírgula.|  
|**validate_subscriber_info**|**nvarchar (500)**|Lista de funções usada para filtrar artigos em uma publicação, onde cada função está separada por um sinal de adição (+).|  
|**uses_host_name**|**bit**|Se a função [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) for usada em filtros de linha com parâmetros, em que **1** significa que essa função é usada para filtragem dinâmica.|  
|**uses_suser_sname**|**bit**|Se a função [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) for usada em filtros de linha com parâmetros, em que **1** significa que essa função é usada para filtragem dinâmica.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_check_dynamic_filters** é usado na replicação de mesclagem.  
  
 Se uma publicação tiver sido definida para usar partições de computação, o **sp_check_dynamic_filters** verificará se há violações das restrições das partições de computação. Se alguma for encontrada, um erro será retornado. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
 Se uma publicação foi definida como tendo filtros de linha com parâmetros, mas nenhum filtro de linha com parâmetros for encontrado, será retornado um erro.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_check_dynamic_filters**.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar partições para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [&#41;&#40;Transact-SQL de sp_check_join_filter ](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_check_subset_filter ](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
