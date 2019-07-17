---
title: sp_validate_redirected_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
author: stevestein
ms.author: sstein
ms.openlocfilehash: dc600aeabd1c988c0f9a6768da7fd0f0d280552b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119424"
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Verifica se o host atual do banco de dados de publicação pode dar suporte à replicação. Deve ser executado em um banco de dados de distribuição. Esse procedimento é chamado pelo **sp_get_redirected_publisher**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'` O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicou originalmente o banco de dados. *original_publisher* está **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` O nome do banco de dados que está sendo publicado. *publisher_db* está **sysname**, sem padrão.  
  
`[ @redirected_publisher = ] 'redirected_publisher'` O destino de redirecionamento especificado quando **sp_redirect_publisher** foi chamado para o par publicador/banco de dados. *redirected_publisher* está **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 nenhuma.  
  
## <a name="remarks"></a>Comentários  
 Se não houver nenhuma entrada para o publicador e o banco de dados de publicação, **sp_validate_redirected_publisher** retorna null no parâmetro de saída *@redirected_publisher* . Se uma entrada existir, ela será retornada no parâmetro de saída nos casos de êxito e de falha.  
  
 Se a validação for bem-sucedida, **sp_validate_redirected_publisher** retorna uma indicação de sucesso.  
  
 Se a validação falhar, ocorrerão erros descrevendo a falha.  
  
## <a name="permissions"></a>Permissões  
 Chamador deve ser um membro do **sysadmin** função de servidor fixa, o **db_owner** função fixa de banco de dados para o banco de dados de distribuição ou membro de uma lista de acesso da publicação para uma publicação definida associado com o banco de dados do publicador.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
