---
title: CREATE APPLICATION ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- APPLICATION_ROLE_TSQL
- CREATE APPLICATION ROLE
- sql13.swb.applicationrole.permissions.f1
- APPLICATION
- APPLICATION ROLE
- CREATE_APPLICATION_ROLE_TSQL
- APPLICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE APPLICATION ROLE statement
- application roles [SQL Server], creating
ms.assetid: 647386da-ee80-41cf-86c9-dd590f9d66b6
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 191d701786ffb4c145aea146da252eb1946f6525
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33066303"
---
# <a name="create-application-role-transact-sql"></a>CREATE APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Adiciona uma função de aplicativo ao banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE APPLICATION ROLE application_role_name   
    WITH PASSWORD = 'password' [ , DEFAULT_SCHEMA = schema_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *application_role_name*  
 Especifica o nome da função de aplicativo. Esse nome ainda não deve ser usado para referenciar qualquer entidade no banco de dados.  
  
 PASSWORD **='***password***'**  
 Especifica a senha que os usuários de banco de dados usam para ativar a função do aplicativo. Você sempre deve usar senhas fortes. A *password* deve atender aos requisitos da política de senha do Windows do computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 DEFAULT_SCHEMA **=***schema_name*  
 Especifica o primeiro esquema que é pesquisado pelo servidor quando ele resolve os nomes de objetos para essa função. Se DEFAULT_SCHEMA for deixado indefinido, a função de aplicativo usará DBO como seu esquema padrão. *schema_name* pode ser um esquema que não existe no banco de dados.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  A complexidade de Senha é verificada quando as senhas de função de aplicativo são definidas. Os aplicativos que invocam funções de aplicativo devem armazenar suas senhas. As senhas de função de aplicativo devem sempre ser criptografadas ao serem armazenadas.  
  
 As funções de aplicativo são visíveis na exibição do catálogo [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md).  
  
 Para obter informações sobre como usar funções de aplicativo, veja [Funções de aplicativo](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma função de aplicativo chamada `weekly_receipts` que tem a senha `987Gbv876sPYY5m23` e `Sales` como esquema padrão.  
  
```  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987G^bv876sPY)Y5m23'   
    , DEFAULT_SCHEMA = Sales;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de Aplicativo](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [Política de senha](../../relational-databases/security/password-policy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
