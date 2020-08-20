---
description: sysdbmaintplan_history (Transact-SQL)
title: sysdbmaintplan_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_history_TSQL
- sysdbmaintplan_history
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_history system table
ms.assetid: 02d36f08-ac93-4463-bb59-284c5cd6ed04
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f5871f6acc8e4df58223e1568b0a253a7e62c42d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473143"
---
# <a name="sysdbmaintplan_history-transact-sql"></a>sysdbmaintplan_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Essa tabela é armazenada no banco de dados **msdb** .  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**sequence_id**|**int**|Sequência de histórico executada por planos de manutenção de banco de dados.|  
|**plan_id**|**uniqueidentifier**|ID do plano de manutenção do banco de dados.|  
|**plan_name**|**sysname**|Nome do plano de manutenção do banco de dados.|  
|**database_name**|**sysname**|Nome do banco de dados associado a esse plano de manutenção do banco de dados.|  
|**server_name**|**sysname**|Nome do sistema.|  
|**activity**|**nvarchar(128)**|Atividade executada pelo plano de manutenção de banco de dados (por exemplo, Log de transação de backup e assim por diante).|  
|**succeeded**|**bit**|**0** = sucesso **1** = falha|  
|**end_time**|**datetime**|Hora em que a ação foi concluída.|  
|**duration**|**int**|Período de tempo necessário para concluir a ação do plano de manutenção do banco de dados.|  
|**start_time**|**datetime**|Hora em que a ação iniciou.|  
|**error_number**|**int**|Número do erro relatado na falha.|  
|**message**|**nvarchar(512)**|Mensagem gerada por **sqlmaint**.|  
  
  
