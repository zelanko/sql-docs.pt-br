---
title: dbo.sysalerts (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
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
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs: TSQL
helpviewer_keywords: sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a28a1152ec3dd85c8bee11c4ef9b73ed3928db27
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada alerta. Um alerta é uma mensagem enviada em resposta a um evento. Um alerta pode encaminhar mensagens além do ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e um alerta pode ser uma mensagem de email ou de pager. Um alerta também pode gerar uma tarefa.  Essa tabela é armazenada no **msdb** banco de dados.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do alerta.|  
|**name**|**sysname**|Nome do alerta.|  
|**origem do evento**|**nvarchar (100)**|Origem do evento: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**event_category_id**|**int**|Reservado para uso futuro.|  
|**event_id**|**int**|Reservado para uso futuro.|  
|**message_id**|**int**|Definido pelo usuário ID da mensagem ou uma referência a **sysmessages** mensagem que dispara esse alerta.|  
|**severidade**|**int**|Severidade que dispara esse alerta.|  
|**habilitado**|**tinyint**|Status do alerta:<br /><br /> **0** = desabilitado.<br /><br /> **1** = habilitado.|  
|**delay_between_responses**|**int**|Período de espera, em segundos, entre as notificações para esse alerta.|  
|**last_occurrence_date**|**int**|Última ocorrência (data) do alerta.|  
|**last_occurrence_time**|**int**|Última ocorrência (hora do dia) do alerta.|  
|**last_response_date**|**int**|Última notificação (data) do alerta.|  
|**last_response_time**|**int**|Última notificação (hora do dia) do alerta.|  
|**notification_message**|**nvarchar(512)**|Informações adicionais enviadas com o alerta.|  
|**include_event_description**|**tinyint**|Bitmask representando se a descrição do evento é enviada por email, Pager ou Net send. Consulte a tabela abaixo para valores.|  
|**database_name**|**nvarchar(512)**|Banco de dados no qual esse alerta deve acontecer para ser disparado.|  
|**event_description_keyword**|**nvarchar (100)**|O padrão do erro deve ser correspondente para que o alerta seja disparado.|  
|**occurrence_count**|**int**|Número de ocorrências para esse alerta.|  
|**count_reset_date**|**int**|Contagem de dias (Data) será redefinida como **0**.|  
|**count_reset_time**|**int**|Hora do dia será redefinida como **0**.|  
|**job_id**|**uniqueidentifier**|ID da tarefa executada quando esse alerta ocorre.|  
|**has_notification**|**int**|Número de operadores que recebem notificação de email quando o alerta ocorre.|  
|**sinalizadores**|**int**|Reservado.|  
|**performance_condition**|**nvarchar(512)**|Reservado.|  
|**category_id**|**int**|Reservado.|  
  
 ## <a name="remarks"></a>Comentários

A tabela a seguir mostra os valores para a máscara de bits de include_event_description. O valor decimal é retornado por dbo.sysalerts. 

|decimal | binary | Significado |
|------|------|------|
|0 |0000 |Nenhuma mensagem |
|1 |0001 |Email |
|2 |0010 |pager |
|3 |0011 |pager e email |
|4 |0100 |Net send |
|5 |0101 |Email e net send |
|6 |0110 |Pager e net send |
|7 |0111 |Email, pager e net send |
  
