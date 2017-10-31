---
title: Parse (mecanismo de banco de dados) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 027940c7575f3c7901cd8668879064ff375d9986
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="parse-database-engine"></a>Parse (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

A análise converte a representação de cadeia de caracteres canônica de um **hierarchyid** para um **hierarchyid** valor. A análise é chamada implicitamente quando uma conversão de um tipo de cadeia de caracteres em **hierarchyid** ocorre. Atua como o oposto do [ToString](../../t-sql/data-types/tostring-database-engine.md). Parse é um método estático.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
## <a name="arguments"></a>Argumentos  
*entrada*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]: o valor do tipo de dados de caractere que está sendo convertido.
  
CLR: o valor String que está sendo avaliado.
  
## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno do SQL Server: hierarchyid**
  
**Tipo de retorno CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Comentários  
Se a análise recebe um valor que não é uma representação de cadeia de caracteres válida de um **hierarchyid**, uma exceção é gerada. Por exemplo, se **char** tipos de dados contém espaços à direita, será gerada uma exceção.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. Convertendo valores Transact-SQL sem uma tabela  
O seguinte exemplo de código usa `ToString` para converter um **hierarchyid** valor em uma cadeia de caracteres e `Parse` para converter um valor de cadeia de caracteres para um **hierarchyid**.
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="b-clr-example"></a>B. Exemplo de CLR  
O trecho de código a seguir chama o método Parse ():
  
```sql
string input = “/1/2/”;  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>Consulte também
[Referência de método de tipo de dados hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

