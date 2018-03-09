---
title: sp_check_join_filter (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords: sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab650e6465ac5c872e90acc890a83d17f286b446
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Será usado para verificar um filtro de junção entre duas tabelas para determinar se a cláusula de filtro de junção é válida. Esse procedimento armazenado também retorna informações sobre o filtro de junção fornecido, incluindo se ele pode ser usado com partições pré-computadas para a tabela determinada. Esse procedimento armazenado é executado no Publicador, na publicação. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@filtered_table** =] **'***filtered_table***'**  
 É o nome de uma tabela filtrada. *filtered_table* é **nvarchar (400)**, sem padrão.  
  
 [  **@join_table** =] **'***join_table***'**  
 É o nome de uma tabela que é adicionada à *filtered_table*. *join_table* é **nvarchar (400)**, sem padrão.  
  
 [  **@join_filterclause**  =] **'***join_filterclause***'**  
 É a cláusula do filtro de junção que está sendo testado. *join_filterclause* é **nvarchar (1000)**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|É se a publicação está qualificada para as partições pré-calculadas; onde **1** significa que partições pré-computadas podem ser usadas, e **0** significa que eles não podem ser usados.|  
|**has_dynamic_filters**|**bit**|Se a cláusula de filtro fornecida inclui pelo menos uma função de filtragem com parâmetros; onde **1** significa que uma função de filtragem com parâmetros é usada, e **0** significa que tal função não é usada.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|Lista de funções na cláusula de filtro que define um filtro com parâmetros para um artigo, onde cada função é separada por um ponto-e-vírgula.|  
|**uses_host_name**|**bit**|Se o [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) função é usada na cláusula de filtro, onde **1** significa que essa função está presente.|  
|**uses_suser_sname**|**bit**|Se o [suser_sname ()](../../t-sql/functions/suser-sname-transact-sql.md) função é usada na cláusula de filtro, onde **1** significa que essa função está presente.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_check_join_filter** é usado em replicação de mesclagem.  
  
 **sp_check_join_filter** pode ser executado em todas as tabelas relacionadas, mesmo se eles não forem publicados. Esse procedimento armazenado pode ser usado para verificar um filtro de junção antes de definir um filtro de junção entre os dois artigos.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_check_join_filter**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
