---
title: sp_check_subset_filter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
author: stevestein
ms.author: sstein
ms.openlocfilehash: fa956275619286c059dacf25a5b9b2b83ed732e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070521"
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  É usado para verificar uma cláusula de filtro em qualquer tabela para determinar se a cláusula é válida para a tabela. Esse procedimento armazenado retorna informações sobre o filtro fornecido, inclusive se o filtro está qualificado para uso com partições pré-computadas. Esse procedimento armazenado é executado no Publicador, no banco de dados que contém a publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filtered_table = ] 'filtered_table'` É o nome de uma tabela filtrada. *filtered_table* está **nvarchar (400)** , sem padrão.  
  
`[ @subset_filterclause = ] 'subset_filterclause'` A cláusula de filtro está sendo testada. *subset_filterclause* está **nvarchar (1000)** , sem padrão.  
  
`[ @has_dynamic_filters = ] has_dynamic_filters` É se a cláusula de filtro é um filtro de linha com parâmetros. *has_dynamic_filters* está **bit**, com um padrão de NULL e é um parâmetro de saída. Retorna um valor de **1** quando a cláusula de filtro é um filtro de linha com parâmetros.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|É se a publicação se qualifica para usar partições pré-computadas; em que **1** significa que as partições pré-calculadas podem ser usadas, e **0** significa que eles não podem ser usados.|  
|**has_dynamic_filters**|**bit**|Se a cláusula de filtro fornecida inclui pelo menos um filtro de linha com parâmetros; em que **1** significa que um filtro de linha com parâmetros é usado, e **0** significa que tal função não é usada.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Lista de funções na cláusula de filtro que filtra dinamicamente um artigo, onde cada função é separada por um ponto e vírgula.|  
|**uses_host_name**|**bit**|Se o [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) função é usada na cláusula de filtro, onde **1** significa que essa função está presente.|  
|**uses_suser_sname**|**bit**|Se o [suser_sname ()](../../t-sql/functions/suser-sname-transact-sql.md) função é usada na cláusula de filtro, onde **1** significa que essa função está presente.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_check_subset_filter** é usado em replicação de mesclagem.  
  
 **sp_check_subset_filter** pode ser executado em qualquer tabela, mesmo se a tabela não for publicada. Esse procedimento armazenado pode ser usado para verificar uma cláusula de filtro antes de definir um artigo filtrado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_check_subset_filter**.  
  
## <a name="see-also"></a>Consulte também  
 [Otimizar o desempenho de filtro parametrizado com partições pré-computadas](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
