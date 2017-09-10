---
title: "AGREGAÇÃO de DROP (Transact-SQL) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a9fcab3dc576f15110bed8c1c82271731f326280
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma função de agregação definida pelo usuário do banco de dados atual. Funções de agregação definida pelo usuário são criadas usando [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente descarta a agregação somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual pertence a função de agregação definida pelo usuário.  
  
 *aggregate_name*  
 É o nome da função de agregação definida pelo usuário que você deseja descartar.  
  
## <a name="remarks"></a>Comentários  
 DROP AGGREGATE não será executado se houver alguma exibição, função ou procedimento armazenado criado com uma ligação de esquema que faça referência à função de agregação definida pelo usuário que você deseja descartar.  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP AGGREGATE, no mínimo, um usuário deve ter permissão ALTER no esquema ao qual pertence a agregação definida pelo usuário ou permissão CONTROL na agregação.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta a agregação `Concatenate`.  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar agregação &#40; Transact-SQL &#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [Criar agregações definidas pelo usuário](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  

