---
title: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b64dc761f5af95ab913291d6aa488ced8fba8cf
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Credencial com escopo de alterações de propriedades de um banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica o nome da credencial no escopo do banco de dados que está sendo alterada.  
  
 IDENTIDADE **='***identity_name***'**  
 Especifica o nome da conta a ser usada ao conectar o servidor externamente. Para importar um arquivo de armazenamento de BLOBs do Azure, o nome de identidade deve ser `SHARED ACCESS SIGNATURE`.  Para obter mais informações sobre assinaturas de acesso compartilhado, consulte [assinaturas usando de acesso compartilhado (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
    
  
 SECRET **='***secret***'**  
 Especifica o segredo necessário para a autenticação de saída. *segredo* é necessária para importar um arquivo de armazenamento de BLOBs do Azure. *segredo* pode ser opcional para outros fins.   
>  [!WARNING]
>  O valor da chave SAS pode começar com um '?' (ponto de interrogação). Quando você usa a chave SAS, você deve remover à esquerda '?'. Caso contrário, seus esforços podem estar bloqueados.    
  
## <a name="remarks"></a>Remarks  
 Quando um banco de dados no escopo credencial é alterada, os valores de *identity_name* e *segredo* são redefinidos. Se o argumento SECRET opcional não for especificado, o valor do segredo armazenado será definido como NULL.  
  
 O segredo é criptografado com a chave mestra de serviço. Se a chave mestra de serviço for gerada novamente, o segredo será criptografado usando a nova chave mestra de serviço.  
  
 Informações sobre credenciais no escopo do banco de dados são visíveis no [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Requer `ALTER` permissão na credencial.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. Credencial com escopo de alteração da senha de um banco de dados  
 O exemplo a seguir altera o segredo armazenado em uma credencial no escopo do banco de dados chamada `Saddles`. A credencial no escopo do banco de dados contém o logon do Windows `RettigB` e sua senha. A nova senha é adicionada à credencial do escopo do banco de dados usando a cláusula SECRET.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Removendo a senha de uma credencial  
 O exemplo a seguir remove a senha de uma credencial no escopo do banco de dados denominada `Frames`. A credencial no escopo do banco de dados contém o logon do Windows `Aboulrus8` e uma senha. Depois que a instrução é executada, a credencial no escopo do banco de dados terá uma senha NULL porque a opção SECRET não foi especificada.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Credenciais &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
