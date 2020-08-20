---
description: sp_audit_write (Transact-SQL)
title: sp_audit_write (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_audit_write
- sp_audit_write_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_audit_write
ms.assetid: 4c523848-1ce6-49ad-92b3-e0e90f24f1c2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9d6d6c6214d4157519454ab4b7eb3eb32ddae360
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469716"
---
# <a name="sp_audit_write-transact-sql"></a>sp_audit_write (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Adiciona um evento de auditoria definido pelo usuário à **USER_DEFINED_AUDIT_GROUP**. Se **USER_DEFINED_AUDIT_GROUP** não estiver habilitado, **sp_audit_write** será ignorado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_audit_write [ @user_defined_event_id = ] user_defined_event_id
    [ , [ @succeeded = ] succeeded ]
    [ , [ @user_defined_information = ] 'user_defined_information' ]
    [ ; ]
```  
  
## <a name="arguments"></a>Argumentos  
 `[ @user_defined_event_id = ] user_defined_event_id`  
 Um parâmetro definido pelo usuário e registrado na coluna **user_defined_event_id** do log de auditoria. * \@ user_defined_event_id* é do tipo **smallint**.  
  
 `[ @succeeded = ] succeeded`  
 Um parâmetro passado por usuário para indicar se o evento teve êxito ou não. Isso aparece na coluna Êxito do log de auditoria. `@succeeded` é **bit**.  
  
 `[ @user_defined_information = ] 'user_defined_information'`  
 É o texto definido pelo usuário e registrado na coluna user_defined_event_id do log de auditoria. `@user_defined_information` é **nvarchar (4000)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
 As falhas são provocadas por parâmetros de entrada incorretos ou erros de gravação no log de auditoria de destino.  
  
## <a name="remarks"></a>Comentários  
 Quando o **USER_DEFINED_AUDIT_GROUP** é adicionado a uma especificação de auditoria de servidor ou uma especificação de auditoria de banco de dados, o evento disparado pelo **sp_audit_write** será incluído no log de auditoria.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-user-defined-audit-event-with-informational-text"></a>a. Criando um evento de auditoria definido pelo usuário com texto informativo  
 O exemplo a seguir cria um evento de auditoria com a id 27, o valor de êxito igual a 0 e o texto informativo opcional incluído.  
  
```  
EXEC sp_audit_write @user_defined_event_id =  27 ,   
              @succeeded =  0   
            , @user_defined_information = N'Access to a monitored object.' ;  
```  
  
### <a name="b--creating-a-user-defined-audit-event-without-informational-text"></a>B.  Criando um evento de auditoria definido pelo usuário sem texto informativo  
 O exemplo a seguir cria um evento de auditoria com a id 27, o valor de êxito igual a 0 e não inclui o texto informativo opcional ou os nomes dos parâmetros opcionais.  
  
```  
EXEC sp_audit_write 27, 0;  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addrole ](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantdbaccess ](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin ](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
