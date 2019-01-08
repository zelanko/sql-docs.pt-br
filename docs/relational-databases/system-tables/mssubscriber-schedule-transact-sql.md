---
title: MSsubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_schedule
- MSsubscriber_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_schedule system table
ms.assetid: ff428306-0ef4-49a3-b536-07ccdf6e2196
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b11ff11d3d5ea8ea98bee18738a7c60450693ef
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202015"
---
# <a name="mssubscriberschedule-transact-sql"></a>MSsubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsubscriber_schedule** tabela contém agendamentos de sincronização transacional para cada par de publicador/assinante e de mesclagem padrão. Esta tabela é armazenada no banco de dados de distribuição.  
  
> [!NOTE]
>  Esta tabela do sistema foi preterida e está sendo mantida para oferecer suporte a versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|O nome do publicador.|  
|**Assinante**|**sysname**|O nome do Assinante.|  
|**agent_type**|**smallint**|O tipo de agente:<br /><br /> 0 = Distribution Agent.<br /><br /> 1 = Merge Agent.|  
|**frequency_type**|**int**|A frequência de agendamento do Distribution Agent:<br /><br /> **1** = uma vez.<br /><br /> **2** = sob demanda.<br /><br /> **4** = diariamente.<br /><br /> **8** = semanalmente.<br /><br /> **16** = mensalmente.<br /><br /> **32** = relativo ao mês.<br /><br /> **64** = iniciar automaticamente.<br /><br /> **128** = recorrente.|  
|**frequency_interval**|**int**|O valor a ser aplicado à frequência definida **frequency_type**.|  
|**frequency_relative_interval**|**int**|A data do Distribution Agent.<br /><br /> **1** = primeiro.<br /><br /> **2** = segundo.<br /><br /> **4** = terceiro.<br /><br /> **8** = quarto.<br /><br /> **16** = último.|  
|**frequency_recurrence_factor**|**int**|O fator de recorrência usado pelo **frequency_type**.|  
|**frequency_subday**|**int**|Frequência de reagendamento durante o período definido:<br /><br /> **1** = uma vez.<br /><br /> **2** = segundo.<br /><br /> **4** = minuto.<br /><br /> **8** = hora.|  
|**frequency_subday_interval**|**int**|O intervalo para **frequency_subday**.|  
|**active_start_time_of_day**|**int**|A hora de dia do primeiro agendamento do Distribution Agent, formatada como HHMMSS.|  
|**active_end_time_of_day**|**int**|A hora do dia em que o Distribution Agent deixa de ser agendado, formatada como HHMMSS.|  
|**active_start_date**|**int**|A data do primeiro agendamento do Distribution Agent, formatada como AAAAMMDD.|  
|**active_end_date**|**int**|A data em que o Distribution Agent deixa de ser agendado, formatada como AAAAMMDD.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
