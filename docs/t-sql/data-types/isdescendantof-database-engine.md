---
title: IsDescendantOf (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f38ee0e89201a1ecc0a8faa145167ad58601c133
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68077818"
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retornará true se *this* for descendente de um pai.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>Argumentos  
*parent*  
O nó **hierarchyid** para o qual o teste IsDescendantOf deve ser executado.
  
## <a name="return-types"></a>Tipos de retorno  
**SQL Server return type:bit**
  
**CLR return type:SqlBoolean**
  
## <a name="remarks"></a>Comentários  
Retornar true para todos os nós na subárvore com raiz em pai e false para todos os outros nós.
  
Pai é considerado seu próprio descendente.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>a. Usando IsDescendantOf em uma cláusula WHERE  
O exemplo a seguir retorna um gerente e os funcionários que pertencem àquele gerente:
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>B. Usando IsDescendantOf para avaliar uma relação  
O código a seguir declara e popula três variáveis. Depois, ele avalia a relação hierárquica e retorna um dos dois resultados impressos com base na comparação:
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. Chamando um método de Common Language runtime  
O snippet de código a seguir chama o método `IsDescendantOf()`.
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>Confira também
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
