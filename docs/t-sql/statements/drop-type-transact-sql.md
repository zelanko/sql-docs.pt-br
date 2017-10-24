---
title: TIPO de DROP (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4187c6bff08e5502f5edc6acd8d82334684a68d4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-type-transact-sql"></a>DROP TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove do banco de dados atual um tipo de dados de alias ou um tipo CLR (Common Language Runtime) definido pelo usuário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente descarta o tipo somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual pertence o alias ou o tipo definido pelo usuário.  
  
 *type_name*  
 É o nome do tipo de dados de alias ou do tipo definido pelo usuário que você deseja descartar.  
  
## <a name="remarks"></a>Comentários  
 A instrução DROP TYPE não será executada quando qualquer um dos seguintes for verdadeiro:  
  
-   Há tabelas no banco de dados que contêm colunas do tipo de dados de alias ou do tipo definido pelo usuário. Informações sobre colunas de tipo definido pelo usuário ou alias podem ser obtidas consultando o [Columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) ou [column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md) exibições do catálogo.  
  
-   Há colunas computadas, restrições CHECK, exibições associadas ao esquema e funções associadas ao esquema cujas definições fazem referência ao alias ou ao tipo definido pelo usuário. Informações sobre essas referências podem ser obtidas consultando o [sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) exibição do catálogo.  
  
-   Há funções, procedimentos armazenados ou disparadores criados no banco de dados, e essas rotinas usam variáveis e parâmetros do alias ou do tipo definido pelo usuário. Informações sobre parâmetros de tipo definido pelo usuário ou alias podem ser obtidas consultando o [sys. Parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) ou [parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md) exibições do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CONTROL em *type_name* ou a permissão ALTER na *schema_name*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir supõe que um tipo denominado `ssn` já esteja criado no banco de dados atual.  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

