---
title: sp_depends (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_depends
- sp_depends_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_depends
ms.assetid: d9934590-c6ae-4936-91c3-146055ef2c57
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f10445e28fd8f0a23d5dcf3f11208cbb733bcc49
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spdepends-transact-sql"></a>sp_depends (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre dependências de objeto de banco de dados, como as exibições e procedimentos que dependem de uma tabela ou exibição e, as tabelas e exibições que dependem da exibição ou procedimento. Não são informadas referências para objetos fora do banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md) e [sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_depends [ @objname = ] '<object>'   
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name.  
    object_name  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual o objeto pertence.  
  
 *object_name*  
 É o objeto de banco de dados que será examinado para verificar se há dependências. O objeto pode ser uma tabela, exibição, procedimento armazenado, função definida pelo o usuário ou gatilho. o*bject_name* é **nvarchar(776)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_depends** exibe dois conjuntos de resultados.  
  
 O conjunto de resultados a seguir mostra os objetos que  *\<objeto >* depende.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (257** **)**|Nome do item para o qual uma dependência existe.|  
|**tipo**|**nvarchar(16)**|Tipo do item.|  
|**atualizado**|**nvarchar(7)**|Caso o item seja atualizado.|  
|**selecionado**|**nvarchar (8)**|Se o item é usado em uma instrução SELECT.|  
|**coluna**|**sysname**|Coluna ou parâmetro em que a dependência existe.|  
  
 O conjunto de resultados a seguir mostra os objetos que dependem de  *\<objeto >*.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (257** **)**|Nome do item para o qual uma dependência existe.|  
|**tipo**|**nvarchar(16)**|Tipo do item.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-dependencies-on-a-table"></a>A. Listando as dependências em uma tabela  
 O exemplo a seguir lista os objetos de banco de dados que dependem da tabela `Sales.Customer` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. São especificados o nome do esquema e da tabela.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_depends @objname = N'Sales.Customer' ;  
```  
  
### <a name="b-listing-dependencies-on-a-trigger"></a>B. Listando as dependências de um gatilho  
 O exemplo a seguir lista os objetos de banco de dados dos quais o gatilho depende `iWorkOrder`.  
  
```  
EXEC sp_depends @objname = N'AdventureWorks2012.Production.iWorkOrder' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sql_dependencies &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
