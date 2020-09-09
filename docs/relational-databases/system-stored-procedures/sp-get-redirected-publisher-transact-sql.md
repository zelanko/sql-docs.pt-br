---
description: sp_get_redirected_publisher (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a71799e3d7820ce4a142d6c9ec7d55b743214fb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538901"
---
# <a name="sp_get_redirected_publisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Usado por agentes de replicação consultar um distribuidor para determinar se o publicador original foi redirecionado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'` O nome da instância do SQL Server que originalmente publicou o banco de dados. *original_publisher* é **sysname**, sem padrão.
  
`[ @publisher_db = ] 'publisher_db'` O nome do banco de dados que está sendo publicado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @bypass_publisher_validation = ] [0 | 1 ]` Usado para ignorar a validação do Publicador Redirecionado. Se for 0, a validação será executada. Se 1, a validação não é executada. *bypass_publisher_validation* é **bit**, com um padrão de 0.  
  
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
 *redirected_publisher* retorna o nome do Publicador atual. Retornará NULL se o Publicador e os bancos de dados de publicação não tiverem sido redirecionados usando **sp_redirect_publisher**.  
  
 Se a validação não for solicitada ou se não existir nenhuma entrada para o Publicador e o banco de dados de publicação, *ERROR_NUMBER* e *ERROR_SEVERITY* retornará 0 e *ERROR_MESSAGE* retornará NULL.  
  
 Se a validação for solicitada, o procedimento armazenado de validação [sp_validate_redirected_publisher &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) for chamado para verificar se o destino do redirecionamento é um host adequado para o banco de dados de publicação. Se a validação for realizada com sucesso, **sp_get_redirected_publisher** retornará o nome do Publicador Redirecionado, 0 para as colunas *ERROR_NUMBER* e *error_severity* e nulo na coluna *ERROR_MESSAGE* .  
  
 Se a validação for solicitada e falhar, o nome do publicador redirecionado será retornado junto com informações de erro.  
  
## <a name="permissions"></a>Permissões  
 O chamador deve ser um membro da função de servidor fixa **sysadmin** , a **db_owner** função fixa de banco de dados para o banco de dados de distribuição ou um membro de uma lista de acesso à publicação para uma publicação definida associada ao banco de dados Publicador.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_validate_redirected_publisher ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_redirect_publisher ](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_validate_replica_hosts_as_publishers ](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
