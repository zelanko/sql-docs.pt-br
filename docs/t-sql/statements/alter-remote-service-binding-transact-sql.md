---
title: "ALTERAR a associação de serviço remoto (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER REMOTE SERVICE BINDING
- ALTER_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote service bindings [Service Broker], modifying
- ALTER REMOTE SERVICE BINDING statement
- modifying remote service bindings
ms.assetid: ee620b4a-9375-4eaa-a016-69916c9e1e68
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5352750b43775b53a508b42de17d33a792a40b1b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o usuário associado a uma associação de serviço remoto ou altera a configuração de autenticação anônima para a associação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *binding_name*  
 O nome da associação de serviço remoto a ser alterada. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
 COM usuário = \< *user_name >*  
 Especifica o usuário de banco de dados que possui o certificado associado ao serviço remoto para esta associação. A chave pública deste certificado é usada para criptografia e autenticação de mensagens trocadas com o serviço remoto.  
  
 ANONYMOUS  
 Especifica se a autenticação anônima é usada durante a comunicação com o serviço remoto. Se ANONYMOUS = ON, a autenticação anônima será usada e as credenciais do usuário local não serão transferidas para o serviço remoto. Se ANONYMOUS = OFF, as credenciais de usuário serão tranferidas. Se essa cláusula não for especificada, o padrão será OFF.  
  
## <a name="remarks"></a>Comentários  
 A chave pública no certificado associado *user_name* é usado para autenticar as mensagens enviadas para o serviço remoto e para criptografar uma chave de sessão que é usada para criptografar a conversa. O certificado para *user_name* deve corresponder ao certificado para um logon no banco de dados que hospeda o serviço remoto.  
  
## <a name="permissions"></a>Permissões  
 Permissão para alterar uma associação de serviço remoto assume como padrão o proprietário do serviço remoto associação, os membros do **db_owner** fixo de função de banco de dados e membros do **sysadmin** função de servidor fixa.  
  
 O usuário que executa a instrução ALTER REMOTE SERVICE BINDING deve ter a permissão de representação para o usuário especificado na instrução.  
  
 Para alterar AUTHORIZATION para uma associação de serviço remoto, use a instrução ALTER AUTHORIZATION.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera a associação de serviço remoto `APBinding` para criptografar mensagens usando os certificados da conta `SecurityAccount`.  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [Remova a associação de serviço remoto &#40; Transact-SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
