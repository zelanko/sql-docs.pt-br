---
title: SET NOEXEC (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NOEXEC_TSQL
- SET_NOEXEC_TSQL
- SET NOEXEC
- NOEXEC
dev_langs:
- TSQL
helpviewer_keywords:
- queries [SQL Server], compiling
- SET NOEXEC statement
- compiling queries [SQL Server]
- NOEXEC option
ms.assetid: ba56fba1-af9b-4459-b6e4-5d7e71a7630b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cf9d59e47fd7d8ebcfe9782ef7469e6348076f9f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="set-noexec-transact-sql"></a>SET NOEXEC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Compila cada consulta mas não a executa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET NOEXEC { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentários  
 Quando SET NOEXEC é ON, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compila cada lote de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], mas não as executa. Quando SET NOEXEC é OFF, todos os lotes são executados depois de compilação.  
  
 A execução de instruções no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem duas fases: compilação e execução. Esta configuração é útil para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valide a sintaxe e os nomes de objeto no código [!INCLUDE[tsql](../../includes/tsql-md.md)] durante a execução. Também é útil para depurar instruções que geralmente fariam parte de um lote maior de instruções.  
  
 A configuração de SET NOEXEC é definida na execução ou em tempo de execução e não no momento da análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `NOEXEC` com uma consulta válida, um consulta com um nome de objeto que não é válido e uma consulta com sintaxe incorreta.  
  
```  
USE AdventureWorks2012;  
GO  
PRINT 'Valid query';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Inner join.  
SELECT e.BusinessEntityID, e.JobTitle, v.Name  
FROM HumanResources.Employee AS e   
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
  
PRINT 'Invalid object name';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Function name uses is a reserved keyword.  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.Values(@BusinessEntityID int)  
RETURNS TABLE  
AS  
RETURN (SELECT PurchaseOrderID, TotalDue  
   FROM dbo.PurchaseOrderHeader  
   WHERE VendorID = @BusinessEntityID);  
  
-- SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
  
PRINT 'Invalid syntax';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Built-in function incorrectly invoked.  
SELECT *  
FROM fn_helpcollations;  
-- Reset SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  
