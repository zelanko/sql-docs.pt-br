---
title: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: dda82977f16ffb710683cba7f880d9b60a9609c3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997408"
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Altera as propriedades de uma credencial no escopo do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica o nome da credencial no escopo do banco de dados que está sendo alterada.  
  
 IDENTITY **='***identity_name***'**  
 Especifica o nome da conta a ser usada ao conectar o servidor externamente. Para importar um arquivo do armazenamento de Blobs do Azure, o nome de identidade deve ser `SHARED ACCESS SIGNATURE`.  Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
    
  
 SECRET **='***secret***'**  
 Especifica o segredo necessário para a autenticação de saída. *secret* é necessário para importar um arquivo de armazenamento de Blobs do Azure. *secret* pode ser opcional para outros fins.   
>  [!WARNING]
>  O valor da chave SAS pode começar com um '?' (ponto de interrogação). Quando você usa a chave SAS, deve remover o '?' à esquerda. Caso contrário, seus esforços poderão ser bloqueados.    
  
## <a name="remarks"></a>Remarks  
 Quando uma credencial no escopo do banco de dados é alterada, os valores *identity_name* e *secret* são redefinidos. Se o argumento SECRET opcional não for especificado, o valor do segredo armazenado será definido como NULL.  
  
 O segredo é criptografado com a chave mestra de serviço. Se a chave mestra de serviço for gerada novamente, o segredo será criptografado usando a nova chave mestra de serviço.  
  
 Informações sobre credenciais no escopo do banco de dados ficam visíveis na exibição do catálogo [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `ALTER` na credencial.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. Alterando a senha de uma credencial no escopo do banco de dados  
 O exemplo a seguir altera o segredo armazenado em uma credencial no escopo do banco de dados chamada `Saddles`. A credencial no escopo do banco de dados contém o logon do Windows `RettigB` e sua senha. A nova senha é adicionada à credencial no escopo do banco de dados que usa a cláusula SECRET.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. Removendo a senha de uma credencial  
 O exemplo a seguir remove a senha de uma credencial no escopo do banco de dados chamada `Frames`. A credencial no escopo do banco de dados contém o logon do Windows `Aboulrus8` e uma senha. Depois que a instrução for executada, a credencial no escopo do banco de dados terá uma senha NULL porque a opção SECRET não é especificada.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
