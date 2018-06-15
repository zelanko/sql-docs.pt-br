---
title: DROP AGGREGATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e784a0e9cf2c48cb8a4c7d5bb20ac63176d5a3cf
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33700549"
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma função de agregação definida pelo usuário do banco de dados atual. As funções de agregação definidas pelo usuário são criadas usando [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Descarta condicionalmente a agregação somente se ela já existir.  
  
 *schema_name*  
 É o nome do esquema ao qual pertence a função de agregação definida pelo usuário.  
  
 *aggregate_name*  
 É o nome da função de agregação definida pelo usuário que você deseja descartar.  
  
## <a name="remarks"></a>Remarks  
 DROP AGGREGATE não será executado se houver alguma exibição, função ou procedimento armazenado criado com uma ligação de esquema que faça referência à função de agregação definida pelo usuário que você deseja descartar.  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP AGGREGATE, no mínimo, um usuário deve ter permissão ALTER no esquema ao qual pertence a agregação definida pelo usuário ou permissão CONTROL na agregação.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta a agregação `Concatenate`.  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [Criar agregações definidas pelo usuário](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
