---
title: sp_check_dynamic_filters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
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
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 248a5234a0620ce18122723db7bce88c61201758
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32990041"
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre propriedades de filtro de linhas com parâmetros para uma publicação, em específico as funções usadas para gerar uma partição de dados filtrados para uma publicação e se a publicação está qualificada para usar partições pré-computadas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**=] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|É se a publicação está qualificada para usar partições pré-computadas; onde **1** significa que partições pré-calculadas podem ser usadas, e **0** significa que eles não podem ser usados.|  
|**has_dynamic_filters**|**bit**|É se o filtro de pelo menos uma linha com parâmetros foi definido na publicação; onde **1** significa que existem um ou mais filtros de linha com parâmetros, e **0** significa que não existem filtros dinâmicos.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Lista de funções usada para filtrar artigos em uma publicação, onde cada função está separada por um ponto-e-vírgula.|  
|**validate_subscriber_info**|**nvarchar(500)**|Lista de funções usada para filtrar artigos em uma publicação, onde cada função está separada por um sinal de adição (+).|  
|**uses_host_name**|**bit**|Se o [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) função é usada em filtros de linha com parâmetros, onde **1** significa que essa função é usada para filtragem dinâmica.|  
|**uses_suser_sname**|**bit**|Se o [suser_sname ()](../../t-sql/functions/suser-sname-transact-sql.md) função é usada em filtros de linha com parâmetros, onde **1** significa que essa função é usada para filtragem dinâmica.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_check_dynamic_filters** é usado em replicação de mesclagem.  
  
 Se uma publicação tiver sido definida para usar partições pré-computadas, **sp_check_dynamic_filters** verifica violações de restrições de partições pré-calculadas. Se alguma for encontrada, um erro será retornado. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
 Se uma publicação foi definida como tendo filtros de linha com parâmetros, mas nenhum filtro de linha com parâmetros for encontrado, será retornado um erro.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_check_dynamic_filters**.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar partições para uma publicação de mesclagem com filtros com parâmetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
