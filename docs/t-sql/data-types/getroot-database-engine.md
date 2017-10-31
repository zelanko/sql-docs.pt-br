---
title: GetRoot (mecanismo de banco de dados) | Microsoft Docs
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
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4de7e4010400cbf3d192efb3dd6709792d734ba
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="getroot-database-engine"></a>GetRoot (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna a raiz da árvore hierárquica. GetRoot () é um método estático.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  
  
## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno do SQL Server: hierarchyid**
  
**Tipo de retorno CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Comentários  
Usado para determinar o nó raiz em uma árvore hierárquica.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-transact-sql-example"></a>A. Exemplo de Transact-SQL  
O seguinte exemplo retorna a raiz da árvore de hierarquia:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. Exemplo de CLR  
O trecho de código a seguir chama o método GetRoot ():
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>Consulte também
[Referência de método de tipo de dados hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

