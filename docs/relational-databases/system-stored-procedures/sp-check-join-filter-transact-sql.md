---
title: sp_check_join_filter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28589be83c62f705457e990b328be98e88905568
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771269"
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Será usado para verificar um filtro de junção entre duas tabelas para determinar se a cláusula de filtro de junção é válida. Esse procedimento armazenado também retorna informações sobre o filtro de junção fornecido, incluindo se ele pode ser usado com partições pré-computadas para a tabela determinada. Esse procedimento armazenado é executado no Publicador, na publicação. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filtered_table = ] 'filtered_table'`É o nome de uma tabela filtrada. *filtered_table* é **nvarchar (400)** , sem padrão.  
  
`[ @join_table = ] 'join_table'`É o nome de uma tabela que está sendo unida a *filtered_table*. *join_table* é **nvarchar (400)** , sem padrão.  
  
`[ @join_filterclause = ] 'join_filterclause'`É a cláusula de filtro de junção que está sendo testada. *join_filterclause* é **nvarchar (1000)** , sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|É se a publicação for qualificada para partições preputadas; em que **1** significa que as partições precomupted podem ser usadas, e **0** significa que elas não podem ser usadas.|  
|**has_dynamic_filters**|**bit**|É se a cláusula de filtro fornecida incluir pelo menos uma função de filtragem com parâmetros; em que **1** significa que uma função de filtragem com parâmetros é usada e **0** significa que essa função não é usada.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Lista de funções na cláusula de filtro que define um filtro com parâmetros para um artigo, onde cada função é separada por um ponto-e-vírgula.|  
|**uses_host_name**|**bit**|Se a função [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) for usada na cláusula de filtro, em que **1** significa que essa função está presente.|  
|**uses_suser_sname**|**bit**|Se a função [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) for usada na cláusula de filtro, em que **1** significa que essa função está presente.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_check_join_filter** é usado na replicação de mesclagem.  
  
 **sp_check_join_filter** pode ser executado em qualquer tabela relacionada, mesmo se elas não forem publicadas. Esse procedimento armazenado pode ser usado para verificar um filtro de junção antes de definir um filtro de junção entre os dois artigos.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_check_join_filter**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
