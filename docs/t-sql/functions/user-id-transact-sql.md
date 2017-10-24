---
title: USER_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USER_ID
- USER_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- USER_ID function
- identification numbers [SQL Server]
- IDs [SQL Server], databases
- users [SQL Server], database ID numbers
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
ms.assetid: 67fd29bc-eda9-4d4d-b148-5d3659181a43
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a40853c10e17969c78ef88e4b75995e77b8a1bac
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="userid-transact-sql"></a>USER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o número de identificação para um usuário de banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *usuário*  
 É o nome de usuário a ser usado. *usuário* é **nchar**. Se um **char** valor for especificado, ele será convertido implicitamente em **nchar**. Os parênteses são necessários.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 Quando *usuário* for omitido, o usuário atual é assumido. Se o parâmetro contiver a palavra NULL, retornará NULL. Quando USER_ID é chamado depois de EXECUTE AS, USER_ID retorna a ID do contexto representado.  
  
 Quando uma entidade do Windows não é mapeada para um banco de dados específico, o usuário acessa um banco de dados por meio da associação em um grupo, USER_ID retorna 0 (a ID de público). Se esse principal criar um objeto sem especificar um esquema, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará um usuário e esquema implícitos mapeados para a entidade de segurança do Windows. O usuário criado em tais casos não pode ser usado para conectar ao banco de dados. As chamadas a USER_ID de um principal do Windows mapeado para um usuário implícito retornarão a ID do usuário implícito.  
  
 USER_ID pode ser usado em uma lista de seleção, em uma cláusula WHERE ou em qualquer local em que uma expressão seja permitida. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o número de identificação para o usuário `AdventureWorks2012` do `Harold`.  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [User_name &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID &#40; Transact-SQL &#41;](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

