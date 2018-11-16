---
title: GetLevel (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 381a1afb5b63ae04e49636a02e890b7ac3e5e112
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698524"
---
# <a name="getlevel-database-engine"></a>GetLevel (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um inteiro que representa a profundidade do nó *this* na árvore.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```sql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  
  
## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno do SQL Server: smallint**
  
**Tipo de retorno do CLR: SqlInt16**
  
## <a name="remarks"></a>Remarks  
Usado para determinar o nível de um ou mais nós ou para filtrar os nós de membros de um nível especificado. A raiz da hierarquia é nível 0.
  
GetLevel é muito útil para índices de pesquisa de primeira amplitude. Para obter mais informações, consulte [Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. Retornando o nível de hierarquia como uma coluna  
O seguinte exemplo retorna uma representação de texto da **hierarchyid** e, em seguida, o nível de hierarquia como a coluna **EmpLevel** para todas as linhas na tabela:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>B. Retornando todos os membros de um nível de hierarquia  
O seguinte exemplo retorna todas as linhas na tabela no nível de hierarquia 2:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>C. Retornando a raiz da hierarquia  
O seguinte exemplo retorna a raiz da árvore do nível de hierarquia:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>D. Exemplo de CLR  
O seguinte snippet de código chama o método GetLevel():
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>Confira também
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
