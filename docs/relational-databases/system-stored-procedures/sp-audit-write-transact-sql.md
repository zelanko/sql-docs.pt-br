---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9bef63c267bdf5b7d0c2603ed7a93af329d1992c
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251975"
---
# <a name="sp_audit_write-transact-sql"></a>sp_audit_write (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Adiciona um evento de auditoria definido pelo usuário ao **USER_DEFINED_AUDIT_GROUP**. Se **USER_DEFINED_AUDIT_GROUP** não estiver habilitado, **sp_audit_write** será ignorado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_audit_write [ @user_defined_event_id = ] user_defined_event_id
    [ , [ @succeeded = ] succeeded ]
    [ , [ @user_defined_information = ] 'user_defined_information' ]
    [ ; ]
```  
  
## <a name="arguments"></a>Argumentos  
 `[ @user_defined_event_id = ] user_defined_event_id`  
 Um parâmetro definido pelo usuário e registrado na coluna **user_defined_event_id** do log de auditoria. *\@user_defined_event_id* é do tipo **smallint**.  
  
 `[ @succeeded = ] succeeded`  
 Um parâmetro passado por usuário para indicar se o evento teve êxito ou não. Isso aparece na coluna Êxito do log de auditoria. `@succeeded` é **bit**.  
  
 `[ @user_defined_information = ] 'user_defined_information'`  
 É o texto definido pelo usuário e registrado na coluna user_defined_event_id do log de auditoria. `@user_defined_information` é **nvarchar (4000)** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
 As falhas são provocadas por parâmetros de entrada incorretos ou erros de gravação no log de auditoria de destino.  
  
## <a name="remarks"></a>Comentários  
 Quando o **USER_DEFINED_AUDIT_GROUP** é adicionado a uma especificação de auditoria de servidor ou uma especificação de auditoria de banco de dados, o evento disparado pelo **sp_audit_write** será incluído no log de auditoria.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-user-defined-audit-event-with-informational-text"></a>A. Criando um evento de auditoria definido pelo usuário com texto informativo  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
