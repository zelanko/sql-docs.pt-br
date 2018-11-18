---
title: GetDescendant (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetDescendant_TSQL
- GetDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- GetDescendant [Database Engine]
ms.assetid: f5f39596-033e-4243-acbc-caa188b45b03
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 64e16514d4f78009522de651f55f8749d6b70319
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51695772"
---
# <a name="getdescendant-database-engine"></a>GetDescendant (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um nó filho do pai.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
parent.GetDescendant ( child1 , child2 )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetDescendant ( SqlHierarchyId child1 , SqlHierarchyId child2 )   
```  
  
## <a name="arguments"></a>Argumentos  
*child1*  
NULL ou a **hierarchyid** de um filho do nó atual.
  
*child2*  
NULL ou a **hierarchyid** de um filho do nó atual.
  
## <a name="return-types"></a>Tipos de retorno  
**Tipo de retorno do SQL Server: hierarchyid**
  
**Tipo de retorno do CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Retorna um nó filho que é um descendente do pai.
-   Se o pai for o NULL, retornará NULL.  
-   Se o pai não for NULL, e child1 e child2 forem NULL, retornará um filho do pai.  
-   Se o pai e child1 não forem NULL e child2 for NULL, retornará um filho do pai maior que child1.  
-   Se o pai e child2 não forem NULL e child1 for NULL, retornará um filho do pai menor que child2.  
-   Se parent, child1 e child2 não forem NULL, retornará um filho do pai maior que child1 e menor que child2.  
-   Se child1 não for NULL e não for um filho de pai, ocorrerá uma exceção.  
-   Se child2 não for NULL e não for um filho de pai, ocorrerá uma exceção.  
-   Se child1 >= child2, ocorrerá uma exceção.  
  
GetDescendant é determinístico. Portanto, se GetDescendant for chamado com as mesmas entradas, sempre produzirá a mesma saída. Contudo, a identidade exata do filho produzida pode variar de acordo com sua relação com os outros nós, como mostrado no exemplo C.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-inserting-a-row-as-the-least-descendant-node"></a>A. Inserindo uma linha como o nó menos descendente  
Um funcionário novo é contratado, subordinado a um funcionário existente no nó `/3/1/`. Execute o seguinte código para inserir a nova linha usando o método GetDescendant sem argumentos para especificar o nó das novas linhas como `/3/1/1/`:
  
```sql
DECLARE @Manager hierarchyid;   
SET @Manager = CAST('/3/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(NULL, NULL),  
'adventure-works\FirstNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="b-inserting-a-row-as-a-greater-descendant-node"></a>B. Inserindo uma linha como um nó mais descendente  
Outro funcionário novo é contratado, subordinado ao mesmo gerente, como no exemplo A. Execute o seguinte código para inserir a nova linha usando o método GetDescendant com o argumento child 1 para especificar que o nó da nova linha virá depois do nó do exemplo A, tornando-se `/3/1/2/`:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, NULL),  
'adventure-works\SecondNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="c-inserting-a-row-between-two-existing-nodes"></a>C. Inserindo uma linha entre dois nós existentes  
Um terceiro funcionário é contratado, subordinado ao mesmo gerente, como no exemplo A. Esse exemplo insere a nova linha em um nó maior que `FirstNewEmployee` no exemplo A e menor que `SecondNewEmployee` no exemplo B. Execute o código a seguir usando o método GetDescendant. Use tanto o argumento child1 como child2 para especificar que o nó da nova linha será o nó `/3/1/1.1/`:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid, @Child2 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
SET @Child2 = CAST('/3/1/2/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, @Child2),  
'adventure-works\ThirdNewEmployee', 'Application Intern', '3/11/07') ;  
  
```  
  
Depois de concluir os exemplos A, B e C, os nós adicionados à tabela serão pares com os seguintes valores de **hierarchyid**:
  
`/3/1/1/`
  
`/3/1/1.1/`
  
`/3/1/2/`
  
O nó `/3/1/1.1/` é maior que o nó `/3/1/1/`, mas está no mesmo nível na hierarquia.
  
### <a name="d-scalar-examples"></a>D. Exemplos de escalar  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a inserções e exclusões arbitrárias de nós **hierarchyid**. Usando GetDescendant(), sempre é possível gerar um nó entre dois nós **hierarchyid**. Execute o código a seguir para gerar nós de exemplo com o uso de `GetDescendant`:
  
```sql
DECLARE @h hierarchyid = hierarchyid::GetRoot();  
DECLARE @c hierarchyid = @h.GetDescendant(NULL, NULL);  
SELECT @c.ToString();  
DECLARE @c2 hierarchyid = @h.GetDescendant(@c, NULL);  
SELECT @c2.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
SET @c = @h.GetDescendant(@c, @c2);  
SELECT @c.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
```  
  
### <a name="e-clr-example"></a>E. Exemplo de CLR  
O snippet de código a seguir chama o método `GetDescendant()`:
  
```sql
SqlHierarchyId parent, child1, child2;  
parent = SqlHierarchyId.GetRoot();  
child1 = parent.GetDescendant(SqlHierarchyId.Null, SqlHierarchyId.Null);  
child2 = parent.GetDescendant(child1, SqlHierarchyId.Null);  
Console.Write(parent.GetDescendant(child1, child2).ToString());  
```  
  
## <a name="see-also"></a>Confira também
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
