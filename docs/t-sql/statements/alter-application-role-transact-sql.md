---
title: "ALTERAR a função de aplicativo (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_APPLICATION_ROLE_TSQL
- ALTER APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying application roles
- passwords [SQL Server], application roles
- ALTER APPLICATION ROLE statement
- application roles [SQL Server], modifying
ms.assetid: c6cd5d0f-18f4-49be-b161-64d9c5569086
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 551e20391cb035cd41eb400e4877fe162d241608
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-application-role-transact-sql"></a>ALTER APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Altera o nome, a senha ou o esquema padrão de uma função de aplicativo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER APPLICATION ROLE application_role_name   
    WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
    NAME = new_application_role_name   
    | PASSWORD = 'password'  
    | DEFAULT_SCHEMA = schema_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *application_role_name*  
 É o nome da função de aplicativo a ser modificada.  
  
 NOME =*new_application_role_name*  
 Especifica o novo nome da função de aplicativo. Esse nome ainda não deve ser usado para referenciar qualquer entidade no banco de dados.  
  
 SENHA ='*senha*'  
 Especifica a senha da função de aplicativo. *senha* devem atender aos requisitos da política de senha do Windows do computador que está executando a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você sempre deve usar senhas fortes.  
  
 DEFAULT_SCHEMA =*schema_name*  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos. *schema_name* pode ser um esquema que não existe no banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Se o novo nome da função de aplicativo já existir no banco de dados, a instrução falhará. Quando o nome, a senha ou o esquema padrão de uma função de aplicativo é alterado, a ID associada à função não é alterada.  
  
> [!IMPORTANT]  
>  A política de expiração de senha não é aplicada às senhas de função de aplicativo. Por esse motivo, tome muito cuidado ao selecionar senhas fortes. Os aplicativos que invocam funções de aplicativo devem armazenar suas senhas.  
  
 As funções de aplicativo são visíveis na exibição do catálogo sys.database_principals.  
  
> [!CAUTION]  
>  Em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]o comportamento de esquemas foi alterado em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O código que pressupõe que esquemas são equivalentes a usuários de banco de dados pode não retornar resultados corretos. Exibições de catálogo antigas, incluindo sysobjects, não devem ser usadas em um banco de dados no qual uma das instruções DDL a seguir já tenha sido utilizada: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. Em um banco de dados no qual qualquer uma dessas instruções tenha sido usada alguma vez, você deve usar as novas exibições do catálogo. As novas exibições do catálogo levam em conta a separação de entidades e esquemas introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para mais informações sobre exibições do catálogo, consulte [Exibições do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados. Para alterar o esquema padrão, o usuário também precisa da permissão ALTER na função de aplicativo. Uma função de aplicativo pode alterar seu próprio esquema padrão, mas não seu nome ou senha.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-name-of-application-role"></a>A. Alterando o nome da função de aplicativo  
 O exemplo a seguir altera o nome da função de aplicativo `weekly_receipts` para `receipts_ledger`.  
  
```  
USE AdventureWorks2012;  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987Gbv8$76sPYY5m23' ,   
    DEFAULT_SCHEMA = Sales;  
GO  
ALTER APPLICATION ROLE weekly_receipts   
    WITH NAME = receipts_ledger;  
GO  
```  
  
### <a name="b-changing-the-password-of-application-role"></a>B. Alterando a senha da função de aplicativo  
 O exemplo a seguir altera a senha da função de aplicativo `receipts_ledger`.  
  
```  
ALTER APPLICATION ROLE receipts_ledger   
    WITH PASSWORD = '897yUUbv867y$200nk2i';  
GO  
```  
  
### <a name="c-changing-the-name-password-and-default-schema"></a>C. Alterando o nome, a senha e o esquema padrão  
 O exemplo a seguir altera o nome, a senha e o esquema padrão da função de aplicativo `receipts_ledger` ao mesmo tempo.  
  
```  
ALTER APPLICATION ROLE receipts_ledger   
    WITH NAME = weekly_ledger,   
    PASSWORD = '897yUUbv77bsrEE00nk2i',   
    DEFAULT_SCHEMA = Production;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de aplicativo](../../relational-databases/security/authentication-access/application-roles.md)   
 [Criar função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Remover função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
