---
title: Parse (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8f7160513cd23e16f06dbba27851920b66bf72c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119822"
---
# <a name="parse-database-engine"></a>Parse (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

O método Parse converte a representação de cadeia de caracteres canônica de uma **hierarchyid** para um valor **hierarchyid**. O método Parse é chamado implicitamente quando ocorre uma conversão de um tipo de cadeia de caracteres em **hierarchyid**. Atua como o oposto de [ToString](../../t-sql/data-types/tostring-database-engine.md). Parse() é um método estático.
  
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
*input*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]: o valor do tipo de dados de caractere que está sendo convertido.
  
CLR: o valor String que está sendo avaliado.
  
## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno do SQL Server: hierarchyid**
  
**Tipo de retorno do CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Se o método Parse receber um valor que não for uma representação de cadeia de caracteres válida de uma **hierarchyid**, será gerada uma exceção. Por exemplo, se tipos de dados **char** contiverem espaços à direita, será gerada uma exceção.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. Convertendo valores Transact-SQL sem uma tabela  
O exemplo de código a seguir usa `ToString` para converter um valor **hierarchyid** em uma cadeia de caracteres e `Parse` para converter um valor de cadeia de caracteres em uma **hierarchyid**.
  
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
O seguinte snippet de código chama o método Parse():
  
```sql
string input = "/1/2/";  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>Confira também
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
