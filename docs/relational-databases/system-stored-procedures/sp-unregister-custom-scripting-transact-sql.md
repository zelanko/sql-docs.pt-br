---
title: sp_unregister_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8d54530c7cf6588a6ae07e1e504e3c53e86f8fa5
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820219"
---
# <a name="sp_unregister_custom_scripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esse procedimento armazenado remove um procedimento armazenado personalizado definido pelo usuário ou um [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script que foi registrado pela execução de [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @type = ] 'type'`É o tipo de procedimento armazenado personalizado ou o script que está sendo removido. o *tipo* é **varchar (16)**, sem padrão, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**inserido**|Procedimento armazenado personalizado registrado ou script executado quando uma instrução INSERT é replicada.|  
|**atualizar**|Procedimento armazenado personalizado registrado ou script executado quando uma instrução UPDATE é replicada.|  
|**delete**|Procedimento armazenado personalizado registrado ou script executado quando uma instrução DELETE é replicada.|  
|**custom_script**|Procedimento armazenado personalizado registrado ou script executado ao término do gatilho DDL (Data Definition Language).|  
  
`[ @publication = ] 'publication'`Nome da publicação para a qual o procedimento armazenado personalizado ou o script está sendo removido. a *publicação* é **sysname**, com um padrão de NULL.  
  
`[ @article = ] 'article'`Nome do artigo para o qual o procedimento armazenado personalizado ou o script está sendo removido. o *artigo* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_unregister_custom_scripting** é usado em instantâneo e replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** ou a função de banco de dados fixa **db_ddladmin** podem ser executados **sp_unregister_custom_scripting**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
