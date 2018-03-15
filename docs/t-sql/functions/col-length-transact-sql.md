---
title: COL_LENGTH (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a5fe2a9da9df8de05f5e4e7f492179445edcf62f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="collength-transact-sql"></a>COL_LENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o comprimento definido, em bytes, de uma coluna.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>Argumentos  
**'** *table* **'**  
É o nome da tabela para a qual determinar as informações de comprimento de coluna. *table* é uma expressão do tipo **nvarchar**.
  
**'** *column* **'**  
É o nome da coluna para a qual determinar as informações de comprimento de coluna. *column* é uma expressão do tipo **nvarchar**.
  
## <a name="return-type"></a>Tipo de retorno
**smallint**
  
## <a name="exceptions"></a>Exceções  
Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.
  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário só pode exibir os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha permissão concedida. Isso significa que as funções internas que emitem metadados, como COL_LENGTH, poderão retornar NULL se o usuário não tiver nenhuma permissão para o objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Remarks  
Para colunas do tipo **varchar** declaradas com o especificador **max** (**varchar(max)**), COL_LENGTH retorna o valor -1.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir mostra os valores de retorno para uma coluna do tipo `varchar(40)` e uma coluna do tipo `nvarchar(40)`.
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 varchar(40), c2 nvarchar(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>Consulte também
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  
