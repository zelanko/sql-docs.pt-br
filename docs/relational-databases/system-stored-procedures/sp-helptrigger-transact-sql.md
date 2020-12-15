---
description: sp_helptrigger (Transact-SQL)
title: sp_helptrigger (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b03afedd01095ddfc233eca9722e9eecde8f840
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468357"
---
# <a name="sp_helptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o tipo ou os tipos de gatilhos DML definidos na tabela especificada para o banco de dados atual. sp_helptrigger não pode ser usado com gatilhos DDL. Consulte a exibição de catálogo de [procedimentos armazenados do sistema](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tabname = ] 'table'` É o nome da tabela no banco de dados atual para o qual retornar informações de gatilho. *Table* é **nvarchar (776)**, sem padrão.  
  
`[ @triggertype = ] 'type'` É o tipo de gatilho DML para o qual retornar informações. o *tipo* é **Char (6)**, com um padrão de NULL e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**DELETE**|Retorna informações do gatilho DELETE.|  
|**INSERT**|Retorna informações do gatilho INSERT.|  
|**UPDATE**|Retorna informações do gatilho UPDATE.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A tabela a seguir mostra as informações contidas no conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|Nome do gatilho.|  
|**trigger_owner**|**sysname**|Nome do proprietário da tabela em que o gatilho é definido.|  
|**isupdate**|**int**|1 = Gatilho UPDATE<br /><br /> 0 = Não é um gatilho UPDATE|  
|**isdelete**|**int**|1 = Gatilho DELETE<br /><br /> 0 = Não é um gatilho DELETE|  
|**isinsert**|**int**|1 = Gatilho INSERT<br /><br /> 0 = Não é um gatilho INSERT|  
|**isafter**|**int**|1 = Gatilho AFTER<br /><br /> 0 = Não é um gatilho AFTER|  
|**isinsteadof**|**int**|1 = Gatilho INSTEAD OF<br /><br /> 0 = Não é um gatilho INSTEAD OF|  
|**trigger_schema**|**sysname**|Nome do esquema ao qual o gatilho pertence.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão de [configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md) na tabela.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir executa `sp_helptrigger` para produzir informações sobre o(s) gatilho(s) na tabela `Person.Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
