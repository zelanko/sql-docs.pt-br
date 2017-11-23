---
title: dbo.sysjobs (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1fd6e90a9e823e38a83f5b218027e15183ab76ae
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena as informações de cada trabalho agendado para ser executado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|A ID exclusiva do trabalho.|  
|**originating_server_id**|**int**|ID do servidor do qual o trabalho originou.|  
|**name**|**sysname**|Nome do trabalho.|  
|**habilitado**|**tinyint**|Indica se o trabalho está habilitado para ser executado.|  
|**Descrição**|**nvarchar(512)**|Descrição do trabalho.|  
|**start_step_id**|**int**|ID da etapa do trabalho em que a execução deve começar.|  
|**category_id**|**int**|ID da categoria de trabalho.|  
|**owner_sid**|**varbinary(85)**|SID (número de identificação de segurança) do proprietário do trabalho.|  
|**notify_level_eventlog**|**int**|**Bitmask** indicando sob quais circunstâncias um evento de notificação deve ser registrado no log de aplicativo do Microsoft Windows:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho for bem-sucedido<br /><br /> **2** = quando o trabalho falhar<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_email**|**int**|Bitmask indicando sob quais circunstâncias um email de notificação deve ser enviado quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho for bem-sucedido<br /><br /> **2** = quando o trabalho falhar<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_netsend**|**int**|Bitmask indicando sob quais circunstâncias uma mensagem de rede deve ser enviada quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho for bem-sucedido<br /><br /> **2** = quando o trabalho falhar<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_page**|**int**|Bitmask indicando sob quais circunstâncias uma página deve ser enviada quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho for bem-sucedido<br /><br /> **2** = quando o trabalho falhar<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_email_operator_id**|**int**|Nome de email do operador a ser notificado.|  
|**notify_netsend_operator_id**|**int**|ID do computador ou usuário usado ao enviar mensagens de rede.|  
|**notify_page_operator_id**|**int**|ID do computador ou usuário usado ao enviar uma página.|  
|**delete_level**|**int**|**Bitmask** indicando sob quais circunstâncias o trabalho deve ser excluído quando um trabalho é concluído:<br /><br /> **0** = nunca<br /><br /> **1** = quando o trabalho for bem-sucedido<br /><br /> **2** = quando o trabalho falhar<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**Date_Created**|**datetime**|Data em que o trabalho foi criado.|  
|**date_modified**|**datetime**|Data em que o trabalho foi modificado pela última vez.|  
|**número_da_versão**|**int**|Versão do trabalho.|  
  
  
