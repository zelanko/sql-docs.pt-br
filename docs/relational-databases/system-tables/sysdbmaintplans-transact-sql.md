---
description: sysdbmaintplans (Transact-SQL)
title: sysdbmaintplans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2b99856c92b13ebfda086a8dea8f2a4bd26e86dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427598"
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta tabela é incluída no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para preservar informações existentes de instâncias atualizadas de uma versão anterior do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não altera o conteúdo dessa tabela. Essa tabela é armazenada no banco de dados **msdb** .  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|ID do plano de manutenção do banco de dados.|  
|**plan_name**|**sysname**|Nome do plano de manutenção do banco de dados.|  
|**date_created**|**datetime**|Data em que o plano de manutenção de banco de dados foi criado.|  
|**proprietário**|**sysname**|Proprietário do plano de manutenção de banco de dados.|  
|**max_history_rows**|**int**|Número máximo de linhas alocado para o registro do histórico do plano de manutenção de banco de dados na tabela de sistema.|  
|**remote_history_server**|**sysname**|Nome do servidor remoto para o qual o relatório de histórico poderia ser escrito.|  
|**max_remote_history_rows**|**int**|Número máximo de linhas alocado na tabela do sistema em um servidor remoto para o qual relatório de histórico poderia ser escrito|  
|**user_defined_1**|**int**|O padrão é NULL.|  
|**user_defined_2**|**nvarchar (100)**|O padrão é NULL.|  
|**user_defined_3**|**datetime**|O padrão é NULL.|  
|**user_defined_4**|**uniqueidentifier**|O padrão é NULL.|  
|**log_shipping**|**bit**|Status de envio de log:<br /><br /> **0** = desabilitado **1** = habilitado|  
  
  
