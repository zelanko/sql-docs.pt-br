---
title: DROP PROCEDURE (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b386dfca28622eb95eec500d909aa7190d081493
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove um ou mais procedimentos armazenados ou grupos de procedimentos do banco de dados atual no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente descarta o procedimento apenas se ele já existe.  
  
 *schema_name*  
 O nome do esquema ao qual o procedimento pertence. Não é possível especificar um nome de servidor ou de banco de dados.  
  
 *procedimento*  
 O nome do procedimento armazenado ou grupo de procedimentos armazenados a ser removido. Não é possível descartar procedimentos individuais em um grupo de procedimentos numerados; todo o grupo de procedimentos é descartado.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Antes de remover qualquer procedimento armazenado, verifique se há objetos dependentes e modifique esses objetos adequadamente. Descartar um procedimento armazenado pode gerar falha de objetos e scripts dependentes quando esses objetos não forem atualizados. Para obter mais informações, consulte [exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
## <a name="metadata"></a>Metadados  
 Para exibir uma lista de procedimentos existentes, consulte o **sys. Objects** exibição do catálogo. Para exibir a definição do procedimento, consulte o **sql_modules** exibição do catálogo.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer **controle** permissão no procedimento, ou **ALTER** permissão no esquema ao qual o procedimento pertence ou associação no **db_ddladmin** função de servidor fixa .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o procedimento armazenado `dbo.uspMyProc` do banco de dados atual.  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 O exemplo a seguir remove vários procedimentos armazenados do banco de dados atual.  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 O exemplo a seguir remove o `dbo.uspMyProc` procedimento armazenado se ele existe, mas não causa um erro se o procedimento não existe. Essa sintaxe é novo no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>Consulte também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Excluir um procedimento armazenado](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  



