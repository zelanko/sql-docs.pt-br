---
title: "EXIBIÇÃO de DROP (Transact-SQL) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8dedeff21f56659d0cc55eef2d133a1ecbe0f63e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove uma ou mais exibições do banco de dados atual. É possível executar DROP VIEW em exibições indexadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]). |  
  
 Condicionalmente descarta o modo de exibição somente se ele já existe.  
  
 *schema_name*  
 É o nome do esquema ao qual a exibição pertence.  
  
 *view_name*  
 É o nome da exibição a ser removida.  
  
## <a name="remarks"></a>Comentários  
 Quando você descarta uma exibição, a definição da exibição e outras informações sobre ela são excluídas do catálogo do sistema. Todas as permissões para a exibição também são excluídas.  
  
 Qualquer exibição em uma tabela descartada pelo uso de DROP TABLE deve ser descartada explicitamente com o uso de DROP VIEW.  
  
 Quando executado em uma exibição indexada, DROP VIEW descarta automaticamente todos os índices em uma exibição. Para exibir todos os índices em uma exibição, use [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
 Ao fazer uma consulta por meio de uma exibição, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se todos os objetos de banco de dados referenciados na instrução existem, se são válidos no contexto da instrução e se as instruções de modificação de dados não violam nenhuma regra de integridade de dados. Uma verificação que falha retorna uma mensagem de erro. Uma verificação com êxito traduz a ação em uma ação na tabela ou tabelas subjacentes. Se as tabelas ou exibições de subjacente tem sido alterado desde a exibição foi criada originalmente, pode ser útil descartar e recriar o modo de exibição.  
  
 Para obter mais informações sobre como determinar dependências para uma exibição específica, consulte [sql_dependencies &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 Para obter mais informações sobre como exibir o texto da exibição, consulte [sp_helptext &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer **controle** permissão na exibição, **ALTER** permissão no esquema que contém a exibição ou associação de **db_ddladmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-drop-a-view"></a>A. Descarta uma exibição  
 O exemplo a seguir remove a exibição `Reorder`.  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Usar &#40; Transact-SQL &#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 

