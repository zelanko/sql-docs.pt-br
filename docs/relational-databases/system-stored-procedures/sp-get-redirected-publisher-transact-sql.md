---
title: sp_get_redirected_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 49bffb24c5ddc45c1c6b88fb424ab419445819fb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529956"
---
# <a name="spgetredirectedpublisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Usado por agentes de replicação consultar um distribuidor para determinar se o publicador original foi redirecionado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'` O nome do banco de dados que está sendo publicado. *publisher_db* está **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` O nome do banco de dados que está sendo publicado. *publisher_db* está **sysname**, sem padrão.  
  
`[ @bypass_publisher_validation = ] [0 | 1 ]` Usado para ignorar a validação do publicador redirecionado. Se for 0, a validação é executada. Se 1, a validação não é executada. *bypass_publisher_validation* está **bit**, com um padrão de 0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|O nome do publicador após o redirecionamento.|  
|**error_number**|**int**|O número do erro de validação.|  
|**error_severity**|**int**|A severidade do erro de validação.|  
|**error_message**|**nvarchar(4000)**|O texto da mensagem de erro de validação.|  
  
## <a name="remarks"></a>Comentários  
 *redirected_publisher* retorna o nome do publicador atual. Retorna null se o publicador e os bancos de dados de publicação não tiverem sido redirecionados usando **sp_redirect_publisher**.  
  
 Se a validação não é solicitada ou se não houver nenhuma entrada para o publicador e o banco de dados de publicação, *error_number* e *error_severity* retornam 0 e *error_message* retorna null.  
  
 Se a validação for solicitada, a procedimento armazenado de validação [sp_validate_redirected_publisher &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) é chamado para verificar se o destino do redirecionamento é um host adequado para a publicação banco de dados. Se a validação for bem-sucedida, **sp_get_redirected_publisher** retorna o nome do publicador redirecionado, 0 para o *error_number* e *error_severity* colunas e null em o *error_message* coluna.  
  
 Se a validação for solicitada e falhar, o nome do publicador redirecionado será retornado junto com informações de erro.  
  
## <a name="permissions"></a>Permissões  
 Chamador deve ser um membro do **sysadmin** função de servidor fixa, o **db_owner** função fixa de banco de dados para o banco de dados de distribuição ou membro de uma lista de acesso da publicação para uma publicação definida associado com o banco de dados do publicador.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
