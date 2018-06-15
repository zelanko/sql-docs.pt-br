---
title: DROP TYPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 48c877b91b1f786a94cb1679d9062f98251ee12d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33067083"
---
# <a name="drop-type-transact-sql"></a>DROP TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove do banco de dados atual um tipo de dados de alias ou um tipo CLR (Common Language Runtime) definido pelo usuário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Remove condicionalmente o tipo somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual pertence o alias ou o tipo definido pelo usuário.  
  
 *type_name*  
 É o nome do tipo de dados de alias ou do tipo definido pelo usuário que você deseja descartar.  
  
## <a name="remarks"></a>Remarks  
 A instrução DROP TYPE não será executada quando qualquer um dos seguintes for verdadeiro:  
  
-   Há tabelas no banco de dados que contêm colunas do tipo de dados de alias ou do tipo definido pelo usuário. É possível obter informações sobre colunas de alias ou de tipo definido pelo usuário consultando as exibições do catálogo [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) ou [sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md).  
  
-   Há colunas computadas, restrições CHECK, exibições associadas ao esquema e funções associadas ao esquema cujas definições fazem referência ao alias ou ao tipo definido pelo usuário. Obtenha informações sobre essas referências consultando a exibição do catálogo [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md).  
  
-   Há funções, procedimentos armazenados ou disparadores criados no banco de dados, e essas rotinas usam variáveis e parâmetros do alias ou do tipo definido pelo usuário. É possível obter informações sobre parâmetros de alias ou de tipo definido pelo usuário consultando as exibições do catálogo [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) ou [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL em *type_name* ou a permissão ALTER em *schema_name*.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir supõe que um tipo denominado `ssn` já esteja criado no banco de dados atual.  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
