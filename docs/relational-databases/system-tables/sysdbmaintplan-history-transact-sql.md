---
title: sysdbmaintplan_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_history_TSQL
- sysdbmaintplan_history
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_history system table
ms.assetid: 02d36f08-ac93-4463-bb59-284c5cd6ed04
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 70afaf6e607f5c8455747a42429f815a6616a8a5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260309"
---
# <a name="sysdbmaintplanhistory-transact-sql"></a>sysdbmaintplan_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Essa tabela é armazenada no **msdb** banco de dados.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**sequence_id**|**Int**|Sequência de histórico executada por planos de manutenção de banco de dados.|  
|**plan_id**|**uniqueidentifier**|ID do plano de manutenção do banco de dados.|  
|**plan_name**|**sysname**|Nome do plano de manutenção do banco de dados.|  
|**database_name**|**sysname**|Nome do banco de dados associado a esse plano de manutenção do banco de dados.|  
|**server_name**|**sysname**|Nome do sistema.|  
|**Atividade**|**nvarchar(128)**|Atividade executada pelo plano de manutenção de banco de dados (por exemplo, Log de transação de backup e assim por diante).|  
|**succeeded**|**bit**|**0** = êxito **1** = falha|  
|**end_time**|**datetime**|Hora em que a ação foi concluída.|  
|**duration**|**Int**|Período de tempo necessário para concluir a ação do plano de manutenção do banco de dados.|  
|**start_time**|**datetime**|Hora em que a ação iniciou.|  
|**error_number**|**Int**|Número do erro relatado na falha.|  
|**message**|**nvarchar(512)**|Mensagem gerada por **sqlmaint**.|  
  
  
