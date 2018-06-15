---
title: dbo.systargetservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f425fb530d10abb4a3285f664b8bed8b083197b8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260702"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra quais servidores de destino estão inscritos atualmente neste domínio de operação multisservidor.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**Int**|ID do servidor.|  
|**server_name**|**sysname**|Nome de servidor.|  
|**local**|**nvarchar(200)**|Local do servidor de destino especificado.|  
|**time_zone_adjustment**|**Int**|Intervalo de ajuste de tempo, em horas, com base na hora de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Data e hora em que o servidor de destino especificado foi inscrito.|  
|**last_poll_date**|**datetime**|Data e hora em que o servidor de destino fez a última sondagem do multisservidor **sysdownloadlist** tabela do sistema para a execução de trabalhos.|  
|**status**|**Int**|Status do servidor de destino:<br /><br /> **1** = Normal<br /><br /> **2** = ressincronização pendente<br /><br /> **4** = suspeito de estar Offline|  
|**local_time_at_last_poll**|**datetime**|Data e hora que o servidor de destino foi sondado pela última vez por operações de trabalho.|  
|**enlisted_by_nt_user**|**nvarchar(100)**|Nome de usuário da pessoa que está executando **sp_msx_enlist** no servidor de destino.|  
|**poll_internal**|**Int**|Número de segundos a serem decorridos antes que o servidor de destino sonde o servidor mestre por novas instruções de carregamento.|  
  
  
