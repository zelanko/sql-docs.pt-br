---
description: ToString (Mecanismo de Banco de Dados)
title: ToString (Mecanismo de Banco de Dados)
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ToString
- ToString_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ToString [Database Engine]
ms.assetid: 5fc11ca5-c26d-4518-9512-67aa0270f110
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1d1460c83488f7ba708f737e7c9bb7bd46819152
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037459"
---
# <a name="tostring-database-engine"></a>ToString (Mecanismo de Banco de Dados)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma cadeia de caracteres com a representação lógica de *this*. ToString é chamado implicitamente quando ocorre uma conversão de **hierarchyid** em um tipo de cadeia de caracteres. Atua como o oposto de [Parse &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/parse-database-engine.md).
  
## <a name="syntax"></a>Sintaxe  

```syntaxsql
-- Transact-SQL syntax
node.ToString  ( )
-- This is functionally equivalent to the following syntax  
-- which implicitly calls ToString():  
CAST(node AS nvarchar(4000))  
```  
  
```syntaxsql
-- CLR syntax
string ToString  ( )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno

**Tipo de retorno do SQL Server: nvarchar(4000)**
  
**Tipo de retorno do CLR: String**
  
## <a name="remarks"></a>Comentários  
Retorna o local lógico na hierarquia. Por exemplo, `/2/1/` representa a quarta linha ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) na seguinte estrutura hierárquica de um sistema de arquivos:
  
```sql
/        C:\  
/1/      C:\Database Files  
/2/      C:\Program Files  
/2/1/    C:\Program Files\Microsoft SQL Server  
/2/2/    C:\Program Files\Microsoft Visual Studio  
/3/      C:\Windows  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-transact-sql-example-in-a-table"></a>a. Exemplo de Transact-SQL em uma tabela  
O seguinte exemplo retorna a coluna `OrgNode` como o tipo de dados **hierarchyid** e no formato de cadeia de caracteres mais legível:
  
```sql
SELECT OrgNode,  
OrgNode.ToString() AS Node  
FROM HumanResources.EmployeeDemo  
ORDER BY OrgNode ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
OrgNode   Node  
0x        /  
0x58      /1/  
0x5AC0    /1/1/  
0x5B40    /1/2/  
0x5BC0    /1/3/  
0x5C20    /1/4/  
...  
```  
  
### <a name="b-converting-transact-sql-values-without-a-table"></a>B. Convertendo valores Transact-SQL sem uma tabela  
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
  
### <a name="c-clr-example"></a>C. Exemplo de CLR  
O seguinte snippet de código chama o método ToString():
  
```sql
this.ToString()  
```  
  
## <a name="see-also"></a>Confira também
[Referência de método de tipo de dados hierarchyid](./hierarchyid-data-type-method-reference.md)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
