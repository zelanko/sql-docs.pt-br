---
title: dbo.sysalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a8addad735c151c38b80af5dfdb46cbf5d66fc3e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada alerta. Um alerta é uma mensagem enviada em resposta a um evento. Um alerta pode encaminhar mensagens além do ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e um alerta pode ser uma mensagem de email ou de pager. Um alerta também pode gerar uma tarefa.  Essa tabela é armazenada no **msdb** banco de dados.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**Int**|ID do alerta.|  
|**name**|**sysname**|Nome do alerta.|  
|**event_source**|**nvarchar(100)**|Origem do evento: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**event_category_id**|**Int**|Reservado para uso futuro.|  
|**event_id**|**Int**|Reservado para uso futuro.|  
|**message_id**|**Int**|Definido pelo usuário ID da mensagem ou uma referência a **sysmessages** mensagem que dispara esse alerta.|  
|**severity**|**Int**|Severidade que dispara esse alerta.|  
|**Habilitado**|**tinyint**|Status do alerta:<br /><br /> **0** = desabilitado.<br /><br /> **1** = habilitado.|  
|**delay_between_responses**|**Int**|Período de espera, em segundos, entre as notificações para esse alerta.|  
|**last_occurrence_date**|**Int**|Última ocorrência (data) do alerta.|  
|**last_occurrence_time**|**Int**|Última ocorrência (hora do dia) do alerta.|  
|**last_response_date**|**Int**|Última notificação (data) do alerta.|  
|**last_response_time**|**Int**|Última notificação (hora do dia) do alerta.|  
|**notification_message**|**nvarchar(512)**|Informações adicionais enviadas com o alerta.|  
|**include_event_description**|**tinyint**|Bitmask representando se a descrição do evento é enviada por email, Pager ou Net send. Consulte a tabela abaixo para valores.|  
|**database_name**|**nvarchar(512)**|Banco de dados no qual esse alerta deve acontecer para ser disparado.|  
|**event_description_keyword**|**nvarchar(100)**|O padrão do erro deve ser correspondente para que o alerta seja disparado.|  
|**occurrence_count**|**Int**|Número de ocorrências para esse alerta.|  
|**count_reset_date**|**Int**|Contagem de dias (Data) será redefinida como **0**.|  
|**count_reset_time**|**Int**|Hora do dia será redefinida como **0**.|  
|**job_id**|**uniqueidentifier**|ID da tarefa executada quando esse alerta ocorre.|  
|**has_notification**|**Int**|Número de operadores que recebem notificação de email quando o alerta ocorre.|  
|**flags**|**Int**|Reservado.|  
|**performance_condition**|**nvarchar(512)**|Reservado.|  
|**category_id**|**Int**|Reservado.|  
  
 ## <a name="remarks"></a>Remarks

A tabela a seguir mostra os valores para a máscara de bits de include_event_description. O valor decimal é retornado por dbo.sysalerts. 

|Decimal | BINARY | Significado |
|------|------|------|
|0 |0000 |Nenhuma mensagem |
|1 |0001 |Email |
|2 |0010 |pager |
|3 |0011 |pager e email |
|4 |0100 |Net send |
|5 |0101 |Email e net send |
|6 |0110 |Pager e net send |
|7 |0111 |Email, pager e net send |
  
