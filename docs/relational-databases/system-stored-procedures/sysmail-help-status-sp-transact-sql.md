---
title: sysmail_help_status_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sysmail_help_status_sp
- sysmail_help_status_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_help_status_sp
ms.assetid: b44277c6-81e8-4b4d-85b3-a2f04d602e7a
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5dcab82374d374eb4a191d91af45c43cba93d9af
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailhelpstatussp-transact-sql"></a>sysmail_help_status_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe o status das filas do Database Mail. Use **sysmail_start_sp** para iniciar as filas do Database Mail e **sysmail_stop_sp** para interromper as filas do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_status_sp  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Status**|**nvarchar(7)**|O status do Database Mail. Os valores possíveis são **iniciado** e **parado**.|  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente os membros do **sysadmin** função de servidor fixa pode acessar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe o status do Database Mail.  
  
```  
EXECUTE msdb.dbo.sysmail_help_status_sp ;  
GO  
```  
  
 Conjunto de resultados:  
  
```  
Status  
-------  
STARTED  
```  
  
## <a name="see-also"></a>Consulte também  
 [Programa externo do Database Mail](../../relational-databases/database-mail/database-mail-external-program.md)   
 [sysmail_start_sp &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [sysmail_stop_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)  
  
  
