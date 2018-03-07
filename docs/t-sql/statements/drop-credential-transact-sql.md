---
title: A CREDENCIAL de DROP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/19/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP CREDENTIAL
- DROP_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing credentials
- DROP CREDENTIAL statement
- credentials [SQL Server], DROP CREDENTIAL statement
- authentication [SQL Server], credentials
- deleting credentials
- dropping credentials
ms.assetid: df22c826-317d-45a6-b078-186acb65f71e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 376d04088502467e0638790ec43ffe6f535c47f0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-credential-transact-sql"></a>DROP CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma credencial do servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 É o nome da credencial a ser removida do servidor.  
  
## <a name="remarks"></a>Comentários  
 Para descartar o segredo associado a uma credencial sem descartar a credencial propriamente dita, use [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md).  
  
 Informações sobre as credenciais são visíveis no **Credentials** exibição do catálogo.  
  
> [!WARNING]  
>  Os proxies são associados com uma credencial. Excluir uma credencial que é usada por um proxy deixa o proxy associado em um estado inutilizável. Ao remover uma credencial usada por um proxy, exclua o proxy (usando [sp_delete_proxy &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md) e recrie o proxy associado usando [sp_add_proxy &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY CREDENTIAL. Se estiver descartando uma credencial de sistema, requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a credencial chamada `Saddles`.  
  
```  
DROP CREDENTIAL Saddles;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Credenciais &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
