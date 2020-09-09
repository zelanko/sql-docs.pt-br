---
description: sp_help_publication_access (Transact-SQL)
title: sp_help_publication_access (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 38ef2fe7710d4716d9b544086f29333c96384bf6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535225"
---
# <a name="sp_help_publication_access-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Retorna uma lista de todos os logons concedidos para uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação a ser acessada. a *publicação* é **sysname**, sem padrão.  
  
`[ @return_granted = ] 'return_granted'` É a ID de logon. *return_granted* é **bit**, com um padrão de 1. Se **0** for especificado e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação for usada, os logons disponíveis que aparecerem no Publicador, mas não no distribuidor serão retornados. Se **0** for especificado e a autenticação do Windows for usada, os logons não negados o acesso especificamente no Publicador ou distribuidor serão retornados.  
  
`[ @login = ] 'login'` É a ID de logon de segurança padrão. o *logon* é **sysname**, com um padrão de **%** .  
  
`[ @initial_list = ] initial_list` Especifica se todos os membros com acesso à publicação devem ser retornados ou apenas aqueles que tinham acesso antes da adição de novos membros à lista. *initial_list* é bit, com um padrão de **0**.  
  
 **1** retorna informações para todos os membros da função de servidor fixa **sysadmin** com logons válidos no distribuidor que existia quando a publicação foi criada, bem como o logon atual.  
  
 **0** retorna informações para todos os membros da função de servidor fixa **sysadmin** com logons válidos no distribuidor que existia quando a publicação foi criada, bem como todos os usuários na lista de acesso à publicação que não pertencem à função de servidor fixa **sysadmin** .  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**LoginName**|**nvarchar(256)**|Nome de logon atual.|  
|**Isntname**|**int**|**0** = o logon não é um usuário do Windows.<br /><br /> **1** = o logon é um usuário do Windows.|  
|**Isntgroup**|**int**|**0** = o logon não é um grupo do Windows.<br /><br /> **1** = o logon é um grupo do Windows.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_help_publication_access** é usado em todos os tipos de replicação.  
  
 Quando **Isntname** e **Isntgroup** no conjunto de resultados são **0**, supõe-se que o logon seja um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_help_publication_access**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_grant_publication_access ](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revoke_publication_access ](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
