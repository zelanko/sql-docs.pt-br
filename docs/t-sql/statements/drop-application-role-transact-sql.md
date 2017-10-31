---
title: "REMOVER a função de aplicativo (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_APPLICATION_ROLE_TSQL
- DROP APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- dropping application roles
- deleting application roles
- removing application roles
- application roles [SQL Server], removing
- DROP APPLICATION ROLE statement
ms.assetid: 44121ee7-ef40-405d-b03b-f8ddb4e3c559
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 326c0bb53e995aeacb807a91b83d69f59d034d2f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-application-role-transact-sql"></a>DROP APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove uma função de aplicativo do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP APPLICATION ROLE rolename  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome de função*  
 Especifica o nome da função de aplicativo a ser descartada.  
  
## <a name="remarks"></a>Comentários  
 Se a função de aplicativo possuir protegíveis, não poderá ser descartada. Antes de descartar uma função de aplicativo que possui itens protegíveis, é necessário transferir a propriedade dos itens protegíveis primeiro ou descartá-los.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 Descartar a função de aplicativo "weekly_ledger" do banco de dados.  
  
```  
DROP APPLICATION ROLE weekly_ledger;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de aplicativo](../../relational-databases/security/authentication-access/application-roles.md)   
 [Criar função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [ALTERAR a função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

