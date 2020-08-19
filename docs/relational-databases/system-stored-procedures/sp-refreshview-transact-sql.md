---
description: sp_refreshview (Transact-SQL)
title: sp_refreshview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refreshview
- sp_refreshview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refreshview
ms.assetid: 9ce1d07c-ee66-4a83-8c73-cd2cc104dd08
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 11b605bd505a88215258afc39c24735d95e56ab6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446899"
---
# <a name="sp_refreshview-transact-sql"></a>sp_refreshview (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Atualiza os metadados para a exibição não associada a esquema. Os metadados persistentes de uma exibição podem tornar-se desatualizados devido a alterações em objetos subjacentes dos quais a exibição depende.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_refreshview [ @viewname = ] 'viewname'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @viewname = ] 'viewname'` É o nome da exibição. *ViewName* é **nvarchar**, sem padrão. *ViewName* pode ser um identificador de várias partes, mas só pode fazer referência a exibições no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha)  
  
## <a name="remarks"></a>Comentários  
 Se uma exibição não for criada com SCHEMABINDING, **sp_refreshview** deverá ser executada quando forem feitas alterações nos objetos subjacentes à exibição que afetam a definição da exibição. Caso contrário, a exibição poderá gerar resultados inesperados quando consultada.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER na exibição e permissão REFERENCES em tipos definidos pelo usuário de common language runtime (CLR) e coleções de esquema XML referenciadas por colunas de exibição.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-updating-the-metadata-of-a-view"></a>a. Atualizando os metadados de uma exibição  
 O exemplo a seguir atualiza os metadados da exibição `Sales.vIndividualCustomer`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sp_refreshview N'Sales.vIndividualCustomer';  
```  
  
### <a name="b-creating-a-script-that-updates-all-views-that-have-dependencies-on-a-changed-object"></a>B. Criando um script que atualiza todas as exibições com dependências de um objeto alterado  
 Considera que a tabela `Person.Person` foi alterada de certo modo que afeta a definição de qualquer exibição criada a partir dela. O exemplo a seguir cria um script que atualiza os metadados de todas as exibições com dependência da tabela `Person.Person`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT 'EXEC sp_refreshview ''' + name + ''''   
FROM sys.objects AS so   
INNER JOIN sys.sql_expression_dependencies AS sed   
    ON so.object_id = sed.referencing_id   
WHERE so.type = 'V' AND sed.referenced_id = OBJECT_ID('Person.Person');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_refreshsqlmodule ](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)  
  
  
