---
description: sp_helpmergefilter (Transact-SQL)
title: sp_helpmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergefilter
- sp_helpmergefilter_TSQL
helpviewer_keywords:
- sp_helpmergefilter
ms.assetid: f133a094-0009-4771-b93b-e86a5c01e40b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: faa3b2922f8d73875b5213603b980560d69465ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526735"
---
# <a name="sp_helpmergefilter-transact-sql"></a>sp_helpmergefilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre filtros de mesclagem. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo. o *artigo* é **sysname**, com um padrão de **%** , que retorna os nomes de todos os artigos.  
  
`[ @filtername = ] 'filtername'` É o nome do filtro sobre o qual retornar informações. *FilterName* é **sysname**, com um padrão de **%** , que retorna informações sobre todos os filtros definidos no artigo ou na publicação.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**int**|ID do filtro de junção.|  
|**filtername**|**sysname**|Nome do filtro.|  
|**join article name**|**sysname**|Nome do artigo de junção.|  
|**join_filterclause**|**nvarchar (2000)**|Cláusula de filtro que qualifica a junção.|  
|**join_unique_key**|**int**|Se a junção está em uma chave exclusiva.|  
|**base table owner**|**sysname**|Nome do proprietário da tabela base.|  
|**base table name**|**sysname**|Nome da tabela base.|  
|**join table owner**|**sysname**|Nome do proprietário da tabela que é adicionada à tabela base.|  
|**join table name**|**sysname**|Nome da tabela que é adicionada à tabela base.|  
|**article name**|**sysname**|Nome do artigo de tabela que é adicionado à tabela base.|  
|**filter_type**|**tinyint**|Tipo de filtro de mesclagem, que pode ser um dos seguintes:<br /><br /> **1** = somente filtro de junção<br /><br /> **2** = relação de registro lógico<br /><br /> **3** = ambos|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergefilter** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** e a função de banco de dados fixa **db_owner** podem executar **sp_helpmergefilter**.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
