---
title: ISJSON (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b641847387801097bce59e78cf75255cc7217be
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Testa se uma cadeia de caracteres contém JSON válido.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 A cadeia de caracteres a ser testada.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna 1 se a cadeia de caracteres contém JSON válido; Caso contrário, retornará 0. Retornará nulo se *expressão* é nulo.  
  
 Não retorna erros.  
  
## <a name="remarks"></a>Comentários  
 **ISJSON** não verifica a exclusividade de chaves no mesmo nível.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example-1"></a>Exemplo 1  
O exemplo a seguir executa um bloco de instruções condicionalmente se o valor do parâmetro `@param` contém JSON válido.  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
 
```  
  
### <a name="example-2"></a>Exemplo 2  
O exemplo a seguir retorna linhas em que a coluna `json_col` contém um JSON válido.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>Consulte também  
 [Dados JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

