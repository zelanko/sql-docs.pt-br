---
title: Remover tabela externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e560c5341abd440f641a988751a6ca2875b9bbb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-table-transact-sql"></a>Remover tabela externa (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Remove uma tabela externa de PolyBase do. Isso não exclui os dados externos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>Argumentos  
 [ *database_name* . [*schema_name*]. | *schema_name* . ] *table_name*  
 O nome de uma a três partes da tabela externa a ser removido. O nome da tabela pode incluir opcionalmente o esquema, ou o banco de dados e esquema.  
  
## <a name="permissions"></a>Permissões  
  
-   Requer **ALTER** permissão no esquema ao qual a tabela pertence.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Descartar uma tabela externa remove todos os metadados da tabela relacionada. Ele não exclui os dados externos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-basic-syntax"></a>A. Usando a sintaxe básica  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>B. Descartando uma tabela externa do banco de dados atual  
 O exemplo a seguir remove o `ProductVendor1` tabela, seus dados, índices e todas as exibições dependentes do banco de dados atual.  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>C. Descartando uma tabela de outro banco de dados  
 O exemplo a seguir descarta a tabela `SalesPerson` no banco de dados `EasternDivision`.  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-basic-syntax"></a>D. Usando a sintaxe básica  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="e-dropping-an-external-table-from-the-current-database"></a>E. Descartando uma tabela externa do banco de dados atual  
 O exemplo a seguir remove o `ProductVendor1` tabela, seus dados, índices e todas as exibições dependentes do banco de dados atual.  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="f-dropping-a-table-from-another-database"></a>F. Descartando uma tabela de outro banco de dados  
 O exemplo a seguir descarta a tabela `SalesPerson` no banco de dados `EasternDivision`.  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  


