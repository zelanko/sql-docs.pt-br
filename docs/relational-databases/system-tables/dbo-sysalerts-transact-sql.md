---
title: dbo. sysalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 277cd9ae3fdbe2414c9c3eb96208e79730ebdde6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813878"
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada alerta. Um alerta é uma mensagem enviada em resposta a um evento. Um alerta pode encaminhar mensagens além do ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e um alerta pode ser uma mensagem de email ou de pager. Um alerta também pode gerar uma tarefa.  Essa tabela é armazenada no banco de dados **msdb** .
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do alerta.|  
|**name**|**sysname**|Nome do alerta.|  
|**event_source**|**nvarchar (100)**|Origem do evento: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**event_category_id**|**int**|Reservado para uso futuro.|  
|**event_id**|**int**|Reservado para uso futuro.|  
|**message_id**|**int**|ID da mensagem definida pelo usuário ou referência à mensagem **sysmessages** que dispara este alerta.|  
|**severity**|**int**|Severidade que dispara esse alerta.|  
|**habilitado**|**tinyint**|Status do alerta:<br /><br /> **0** = desabilitado.<br /><br /> **1** = habilitado.|  
|**delay_between_responses**|**int**|Período de espera, em segundos, entre as notificações para esse alerta.|  
|**last_occurrence_date**|**int**|Última ocorrência (data) do alerta.|  
|**last_occurrence_time**|**int**|Última ocorrência (hora do dia) do alerta.|  
|**last_response_date**|**int**|Última notificação (data) do alerta.|  
|**last_response_time**|**int**|Última notificação (hora do dia) do alerta.|  
|**notification_message**|**nvarchar(512)**|Informações adicionais enviadas com o alerta.|  
|**include_event_description**|**tinyint**|Bitmask que representa se a descrição do evento é enviada por email, pager ou net send. Consulte o gráfico abaixo para obter valores.|  
|**database_name**|**nvarchar(512)**|Banco de dados no qual esse alerta deve acontecer para ser disparado.|  
|**event_description_keyword**|**nvarchar (100)**|O padrão do erro deve ser correspondente para que o alerta seja disparado.|  
|**occurrence_count**|**int**|Número de ocorrências para esse alerta.|  
|**count_reset_date**|**int**|A contagem de dia (Data) será redefinida como **0**.|  
|**count_reset_time**|**int**|A hora do número do dia será redefinida como **0**.|  
|**job_id**|**uniqueidentifier**|ID da tarefa executada quando esse alerta ocorre.|  
|**has_notification**|**int**|Número de operadores que recebem notificação de email quando o alerta ocorre.|  
|**sinalizadores**|**int**|Reservado.|  
|**performance_condition**|**nvarchar(512)**|Reservado.|  
|**category_id**|**int**|Reservado.|  
  
 ## <a name="remarks"></a>Comentários

A tabela a seguir mostra os valores para o include_event_description bitmask. O valor decimal é retornado por dbo. sysalerts. 

|decimal | binary | que significa |
|------|------|------|
|0 |0000 |nenhuma mensagem |
|1 |0001 |email |
|2 |0010 |pager |
|3 |0011 |pager e email |
|4 |0100 |Net send |
|5 |0101 |Net send e email |
|6 |0110 |Net send e pager |
|7 |0111 |Net send, pager e email |
  
