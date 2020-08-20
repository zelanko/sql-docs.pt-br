---
description: dbo.systargetservers (Transact-SQL)
title: dbo.sysTargetServers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9b8391e01d681f50f36a6f0c5b1b13a2726eaae5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488926"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Registra quais servidores de destino estão inscritos atualmente neste domínio de operação multisservidor.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID do servidor.|  
|**server_name**|**sysname**|Nome de servidor.|  
|**local**|**nvarchar(200)**|Local do servidor de destino especificado.|  
|**time_zone_adjustment**|**int**|Intervalo de ajuste de tempo, em horas, com base na hora de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Data e hora em que o servidor de destino especificado foi inscrito.|  
|**last_poll_date**|**datetime**|A data e a hora em que o servidor de destino especificado pesquisou pela última vez a tabela do sistema **sysdownloadlist** do multisservidor para que os trabalhos sejam executados.|  
|**status**|**int**|Status do servidor de destino:<br /><br /> **1** = normal<br /><br /> **2** = nova sincronização pendente<br /><br /> **4** = suspeito offline|  
|**local_time_at_last_poll**|**datetime**|Data e hora que o servidor de destino foi sondado pela última vez por operações de trabalho.|  
|**enlisted_by_nt_user**|**nvarchar (100)**|Nome de usuário da pessoa que está executando **sp_msx_enlist** no servidor de destino.|  
|**poll_internal**|**int**|Número de segundos a serem decorridos antes que o servidor de destino sonde o servidor mestre por novas instruções de carregamento.|  
  
  
