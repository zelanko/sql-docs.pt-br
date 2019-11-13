---
title: sp_rename (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_rename_TSQL
- sp_rename
dev_langs:
- TSQL
helpviewer_keywords:
- renaming indexes
- renaming columns
- sp_rename
- renaming tables
ms.assetid: bc3548f0-143f-404e-a2e9-0a15960fc8ed
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 92ef8c4583db152b2f81a574010a12030680704f
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983067"
---
# <a name="sp_rename-transact-sql"></a>sp_rename (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Altera o nome de um objeto criado pelo usuário no banco de dados atual. Esse objeto pode ser uma tabela, um índice, uma coluna, um tipo de dados de alias ou um tipo CLR ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime) definido pelo usuário.  
  
> [!CAUTION]  
>  A alteração de qualquer parte de um nome de objeto pode quebrar scripts e procedimentos armazenados. É recomendável não usar essa instrução para renomear procedimentos armazenados, gatilhos, funções definidas pelo usuário ou exibições; em vez disso, descarte o objeto e recrie-o com o novo nome.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rename [ @objname = ] 'object_name' , [ @newname = ] 'new_name'   
    [ , [ @objtype = ] 'object_type' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [@objname =] '*object_name*'  
 É o nome atual qualificado ou não qualificado do objeto do usuário ou do tipo de dados. Se o objeto a ser renomeado for uma coluna em uma tabela, *object_name* deverá estar no formato *tabela. coluna* ou *esquema. tabela. coluna*. Se o objeto a ser renomeado for um índice, *object_name* deverá estar no formato *Table. index* ou *Schema. Table. index*. Se o objeto a ser renomeado for uma restrição, *object_name* deverá estar no formato *Schema. Constraint*.  
  
 As aspas serão necessárias apenas se um objeto qualificado estiver especificado. Se um nome completamente qualificado, incluindo um nome de banco de dados, for fornecido, o nome do banco de dados deverá ser o nome do banco de dados atual. *object_name* é **nvarchar (776)** , sem padrão.  
  
 [ @newname = ] '*new_name*'  
 É o novo nome do objeto especificado. *new_name* deve ser um nome de uma parte e deve seguir as regras para identificadores. *NewName* é **sysname**, sem padrão.  
  
> [!NOTE]  
>  Os nomes de gatilhos não podem começar com # ou ##.  
  
 [@objtype =] '*object_type*'  
 É o tipo do objeto que está sendo renomeado. *object_type* é **varchar (13)** , com um padrão de NULL, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|COLUMN|Uma coluna a ser renomeada.|  
|DATABASE|Um banco de dados definido pelo usuário. Esse tipo de objeto é necessário quando um banco de dados é renomeado.|  
|INDEX|Um índice definido pelo usuário. Renomear um índice com estatísticas automaticamente também renomeia as estatísticas.|  
|OBJECT|Um item de um tipo rastreado em [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Por exemplo, OBJECT pode ser usado para renomear objetos, inclusive restrições (CHECK, FOREIGN KEY, PRIMARY/UNIQUE KEY), tabelas de usuário e regras.|  
|STATISTICS|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> As estatísticas criadas explicitamente por um usuário ou criadas implicitamente com um índice. Renomear as estatísticas de um índice automaticamente também renomeia o índice.|  
|USERDATATYPE|Um tipo [CLR definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) adicionado por meio da execução de [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) ou [sp_addtype](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md).|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha)  
  
## <a name="remarks"></a>Remarks  
 Você só pode alterar o nome de um objeto ou tipo de dados no banco de dados atual. Os nomes da maioria dos tipos de dados do sistema e objetos do sistema não podem ser alterados.  
  
 sp_rename renomeia automaticamente o índice associado sempre que uma restrição PRIMARY KEY ou UNIQUE é renomeada. Se um índice renomeado for vinculado a uma restrição PRIMARY KEY, a restrição PRIMARY KEY também será renomeada automaticamente através de sp_rename.  
  
 sp_rename pode ser usado para renomear índices XML primários e secundários.  
  
 Renomear um procedimento armazenado, uma função, uma exibição ou um gatilho não alterará o nome do objeto correspondente na coluna definição da exibição de catálogo [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) ou obtido usando a função interna [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) . Portanto, é recomendável que sp_rename não seja usado para renomear esses tipos de objetos. Em vez disso, cancele e recrie o objeto com o nome novo.  
  
 A renomeação de um objeto, como uma tabela ou coluna, não renomeará automaticamente as referências a esse objeto. É necessário modificar manualmente todos os objetos que fazem referência ao objeto renomeado. Por exemplo, se você renomear uma coluna de tabela e aquela coluna for referenciada em um gatilho, será necessário modificar o gatilho para que ele reflita o nome novo da coluna. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para listar as dependências do objeto antes de renomeá-lo.  
  
## <a name="permissions"></a>Permissões  
 Para renomear objetos, colunas e índices, a permissão ALTER é necessária no objeto. Para renomear tipos de usuário, a permissão CONTROL é necessária no tipo. Para renomear um banco de dados, a associação é necessária nas funções de servidor fixas sysadmin ou dbcreator.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-renaming-a-table"></a>A. Renomeando uma tabela  
 O exemplo a seguir renomeia a tabela `SalesTerritory` como `SalesTerr` no esquema `Sales` .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
GO  
```  
  
### <a name="b-renaming-a-column"></a>b. Renomeando uma coluna  
 O exemplo a seguir renomeia a coluna `TerritoryID` na tabela `SalesTerritory` como `TerrID`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
GO  
```  
  
### <a name="c-renaming-an-index"></a>C. Renomeando um índice  
 O exemplo a seguir renomeia o índice `IX_ProductVendor_VendorID` como `IX_VendorID`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';  
GO  
```  
  
### <a name="d-renaming-an-alias-data-type"></a>D. Renomeando um tipo de dados de alias  
 O exemplo a seguir renomeia o tipo de dados de alias `Phone` como `Telephone`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Phone', N'Telephone', N'USERDATATYPE';  
GO  
```  
  
### <a name="e-renaming-constraints"></a>E. Renomeando restrições  
 Os exemplos a seguir renomeiam uma restrição PRIMARY KEY, uma restrição CHECK e uma restrição FOREIGN KEY. Ao renomear uma restrição, o esquema ao qual ela pertence deve ser especificado.  
  
```  
USE AdventureWorks2012;   
GO  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');   
GO  
  
-- Rename the primary key constraint.  
sp_rename 'HumanResources.PK_Employee_BusinessEntityID', 'PK_EmployeeID';  
GO  
  
-- Rename a check constraint.  
sp_rename 'HumanResources.CK_Employee_BirthDate', 'CK_BirthDate';  
GO  
  
-- Rename a foreign key constraint.  
sp_rename 'HumanResources.FK_Employee_Person_BusinessEntityID', 'FK_EmployeeID';  
  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');  
  
```  
  
```  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_Person_BusinessEntityID   HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_BusinessEntityID          HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_Employee_BirthDate                 HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_ID                        HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_ID                        HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_BirthDate                          HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
```  
  
### <a name="f-renaming-statistics"></a>F. Renomeando estatísticas  
 O exemplo a seguir cria um objeto de estatísticas chamado contactMail1 e, em seguida, renomeia a estatística para NewContact usando sp_rename. Ao renomear estatísticas, o objeto deve ser especificado no formato schema.table.statistics_name.  
  
```  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
  
sp_rename 'Person.Person.ContactMail1', 'NewContact','Statistics';  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos &#40;armazenados TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
