---
title: sp_mergemetadataretentioncleanup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1797200ce5369f49035f1a950d606e34e584edc2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658413"
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Executa uma limpeza manual de metadados na [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_ mapeamentos](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), e [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) tabelas do sistema. Esse procedimento armazenado é executado em cada Publicador e Assinante na topologia.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT` Retorna o número de linhas limpas dos [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) tabela. *num_genhistory_rows* está **int**, com um padrão de **0**.  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT` Retorna o número de linhas limpas dos [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabela. *num_contents_rows* está **int**, com um padrão de **0**.  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT` Retorna o número de linhas limpas dos [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabela. *num_tombstone_rows* está **int**, com um padrão de **0**.  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only` Somente para uso interno.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]  
>  Se houver várias publicações em um banco de dados e qualquer uma dessas publicações usa um período de retenção de publicação infinito, executando **sp_mergemetadataretentioncleanup** não limpará o controle de alterações a replicação de mesclagem metadados para o banco de dados. Por esse motivo, use a retenção de publicação infinita com precaução. Para determinar se uma publicação tem um período de retenção infinito, execute [sp_helpmergepublication &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) no publicador e observe qualquer publicação no resultado definido com um valor de **0** para **retenção**.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **db_owner** fixo de função de banco de dados ou os usuários na lista de acesso à publicação de um banco de dados publicado pode executar **sp_mergemetadataretentioncleanup**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
