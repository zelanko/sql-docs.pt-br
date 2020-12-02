---
description: ALTER REMOTE SERVICE BINDING (Transact-SQL)
title: ALTER REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 47c4e18c28a5377fa487e0d4d4e8b9be4cf58acc
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128066"
---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera o usuário associado a uma associação de serviço remoto ou altera a configuração de autenticação anônima para a associação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *binding_name*  
 O nome da associação de serviço remoto a ser alterada. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
 WITH USER = \<*user_name>*  
 Especifica o usuário de banco de dados que possui o certificado associado ao serviço remoto para esta associação. A chave pública deste certificado é usada para criptografia e autenticação de mensagens trocadas com o serviço remoto.  
  
 ANONYMOUS  
 Especifica se a autenticação anônima é usada durante a comunicação com o serviço remoto. Se ANONYMOUS = ON, a autenticação anônima será usada e as credenciais do usuário local não serão transferidas para o serviço remoto. Se ANONYMOUS = OFF, as credenciais de usuário serão tranferidas. Se essa cláusula não for especificada, o padrão será OFF.  
  
## <a name="remarks"></a>Comentários  
 A chave pública no certificado associado a *user_name* é usada para autenticar as mensagens enviadas ao serviço remoto e para criptografar uma chave da sessão que, em seguida, é usada para criptografar a conversa. O certificado para *user_name* deve corresponder ao certificado para um logon no banco de dados que hospeda o serviço remoto.  
  
## <a name="permissions"></a>Permissões  
 A permissão para alterar uma associação de serviço remoto usa como padrão o proprietário da associação de serviço remoto, os membros da função de banco de dados fixa **db_owner** e os membros da função de servidor fixa **sysadmin**.  
  
 O usuário que executa a instrução ALTER REMOTE SERVICE BINDING deve ter a permissão de representação para o usuário especificado na instrução.  
  
 Para alterar AUTHORIZATION para uma associação de serviço remoto, use a instrução ALTER AUTHORIZATION.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera a associação de serviço remoto `APBinding` para criptografar mensagens usando os certificados da conta `SecurityAccount`.  
  
```sql  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
