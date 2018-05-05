---
title: sysdbmaintplans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d4f8b7c90d644cb9153bf716e91c38c56bee7f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta tabela está incluída no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para preservar informações existentes de instâncias atualizadas de uma versão anterior do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não altera o conteúdo dessa tabela. Essa tabela é armazenada no **msdb** banco de dados.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|ID do plano de manutenção do banco de dados.|  
|**plan_name**|**sysname**|Nome do plano de manutenção do banco de dados.|  
|**date_created**|**datetime**|Data em que o plano de manutenção de banco de dados foi criado.|  
|**proprietário**|**sysname**|Proprietário do plano de manutenção de banco de dados.|  
|**max_history_rows**|**Int**|Número máximo de linhas alocado para o registro do histórico do plano de manutenção de banco de dados na tabela de sistema.|  
|**remote_history_server**|**sysname**|Nome do servidor remoto para o qual o relatório de histórico poderia ser escrito.|  
|**max_remote_history_rows**|**Int**|Número máximo de linhas alocado na tabela do sistema em um servidor remoto para o qual relatório de histórico poderia ser escrito|  
|**user_defined_1**|**Int**|O padrão é NULL.|  
|**user_defined_2**|**nvarchar(100)**|O padrão é NULL.|  
|**user_defined_3**|**datetime**|O padrão é NULL.|  
|**user_defined_4**|**uniqueidentifier**|O padrão é NULL.|  
|**log_shipping**|**bit**|Status de envio de log:<br /><br /> **0** = disabled **1** = habilitado|  
  
  
