---
title: GetRoot (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4dfb1988f2f1405b2e69459824ee47983295ad31
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556196"
---
# <a name="getroot-database-engine"></a>GetRoot (Mecanismo de Banco de Dados)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna a raiz da árvore hierárquica. GetRoot() é um método estático.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno do SQL Server: hierarchyid**
  
**Tipo de retorno do CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Comentários  
Usado para determinar o nó raiz em uma árvore hierárquica.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-transact-sql-example"></a>a. Exemplo de Transact-SQL  
O seguinte exemplo retorna a raiz da árvore de hierarquia:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. Exemplo de CLR  
O seguinte snippet de código chama o método GetRoot():
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>Confira também
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
