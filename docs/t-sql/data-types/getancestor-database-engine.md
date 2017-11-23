---
title: GetAncestor (mecanismo de banco de dados) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetAncestor_TSQL
- GetAncestor
dev_langs:
- TSQL
helpviewer_keywords:
- GetAncestor [Database Engine]
ms.assetid: b96a986f-d5e4-4034-8013-de7974594ee9
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7649b3290175787b293ea1b720bb299ead89971
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="getancestor-database-engine"></a>GetAncestor (Mecanismo do Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **hierarchyid** que representa o  *n* º ancestral *isso*.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
child.GetAncestor ( n )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetAncestor ( int n )  
```  
  
## <a name="arguments"></a>Argumentos  
*n*  
Um **int**, que representa o número de níveis para subir na hierarquia.
  
## <a name="return-types"></a>Tipos de retorno
**Tipo de retorno do SQL Server: hierarchyid**
  
**Tipo de retorno CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Comentários  
Usado para testar se cada nó da saída possui o nó atual como um ancestral no nível específico.
  
Se um número maior que [GetLevel ()](../../t-sql/data-types/getlevel-database-engine.md) é passado, NULL será retornado.
  
Se um número negativo for passado, ocorrerá uma exceção.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-the-child-nodes-of-a-parent"></a>A. Localizando os nós filho de um pai  
`GetAncestor(1)` retorna os funcionários que têm `david0` como o ancestral imediato (seu pai). O exemplo a seguir usa `GetAncestor(1)`.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(1) = @CurrentEmployee ;  
```  
  
### <a name="b-returning-the-grandchildren-of-a-parent"></a>B. Retornando os netos de um pai  
`GetAncestor(2)` retorna os funcionários que estão dois níveis abaixo na hierarquia a partir do nó atual. Estes são os netos do nó atual. O exemplo a seguir usa `GetAncestor(2)`.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\ken0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(2) = @CurrentEmployee ;  
```  
  
### <a name="c-returning-the-current-row"></a>C. Retornando a linha atual  
Para retornar o nó atual usando `GetAncestor(0)`, execute o seguinte código.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(0) = @CurrentEmployee ;  
```  
  
### <a name="d-returning-a-hierarchy-level-if-a-table-is-not-present"></a>D. Retornando um nível de hierarquia se uma tabela não existir  
`GetAncestor` retornará o nível selecionado na hierarquia mesmo que não haja uma tabela. Por exemplo, o código a seguir designa um funcionário atual e retorna a `hierarchyid` do ancestral do funcionário atual sem fazer referência à uma tabela.
  
```sql
DECLARE @CurrentEmployee hierarchyid ;  
DECLARE @TargetEmployee hierarchyid ;  
SELECT @CurrentEmployee = '/2/3/1.2/5/3/' ;  
SELECT @TargetEmployee = @CurrentEmployee.GetAncestor(2) ;  
SELECT @TargetEmployee.ToString(), @TargetEmployee ;  
```  
  
### <a name="e-calling-a-common-language-runtime-method"></a>E. Chamando um método de tempo de execução de linguagem comum  
O trecho de código a seguir chama o método `GetAncestor()`.
  
```sql
this.GetAncestor(1)  
```  
  
## <a name="see-also"></a>Consulte também
[IsDescendantOf &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/isdescendantof-database-engine.md)  
[Referência de método de tipo de dados hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

