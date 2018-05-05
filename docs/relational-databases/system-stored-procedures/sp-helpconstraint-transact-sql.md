---
title: sp_helpconstraint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpconstraint
- sp_helpconstraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpconstraint
ms.assetid: 29d6cd36-535d-4765-bca8-62f9d9886ff5
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0ec7742d8c51b26618456ca8d9a499331f403dff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpconstraint-transact-sql"></a>sp_helpconstraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma lista de todos os tipos de restrição, seu nome definido pelo usuário ou fornecido pelo sistema, as colunas com base nas quais elas foram definidas e a expressão que define a restrição (somente para restrições DEFAULT e CHECK).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpconstraint [ @objname = ] 'table'   
     [ , [ @nomsg = ] 'no_message' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname=** ] **'***tabela***'**  
 É a tabela sobre a qual as informações de restrição são retornadas. A tabela especificada deve ser local ao banco de dados atual. *tabela* é **nvarchar(776)**, sem padrão.  
  
 [  **@nomsg=**] **'***no_message***'**  
 É um parâmetro opcional que imprime o nome da tabela. *no_message* é **varchar(5)**, com um padrão de **msg**. **nomsg** suprime a impressão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_helpconstraint** exibe uma coluna indexada decrescente se ela participou de chaves primárias. A coluna indexada de maneira decrescente será listada no conjunto de resultados com um sinal de menos (-) após seu nome. O padrão, uma coluna indexada de maneira crescente, será listada apenas por seu nome.  
  
## <a name="remarks"></a>Remarks  
 Executar **sp_help * tabela* relata todas as informações sobre a tabela especificada. Para ver as informações de restrição, use **sp_helpconstraint**.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra todas as restrições da tabela `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpconstraint 'Production.Product';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. CHECK_CONSTRAINTS &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys. default_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)  
  
  
