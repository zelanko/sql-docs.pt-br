---
description: sysmail_help_status_sp (Transact-SQL)
title: sysmail_help_status_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_status_sp
- sysmail_help_status_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_status_sp
ms.assetid: b44277c6-81e8-4b4d-85b3-a2f04d602e7a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 53f0512a2d6d57606a146c39325692b9c3d351e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469151"
---
# <a name="sysmail_help_status_sp-transact-sql"></a>sysmail_help_status_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe o status das filas do Database Mail. Use **sysmail_start_sp** para iniciar as filas de Database Mail e **sysmail_stop_sp** para interromper as filas de Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_status_sp  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Status**|**nvarchar (7)**|O status do Database Mail. Os valores possíveis são **iniciados** e **interrompidos**.|  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente os membros da função de servidor fixa **sysadmin** podem acessar esse procedimento.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail programa externo](../../relational-databases/database-mail/database-mail-external-program.md)   
 [&#41;&#40;Transact-SQL de sysmail_start_sp ](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [sysmail_stop_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)  
  
  
