---
title: managed_backup.sp_get_backup_diagnostics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_get_backup_diagnostics_TSQL
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics_TSQL
- smart_admin.sp_get_backup_diagnostics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics
ms.assetid: 2266a233-6354-464b-91ec-824ca4eb9ceb
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2b2f8c78b1802ff177040352cd7342b51b035c6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38051314"
---
# <a name="managedbackupspgetbackupdiagnostics-transact-sql"></a>managed_backup.sp_get_backup_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna Eventos Estendidos registrados pelo Smart Admin.  
  
 Use este procedimento armazenado para monitorar eventos estendidos registrados pelo Smart Admin. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] eventos são registrados neste sistema e podem ser examinados e monitorados usando esse procedimento armazenado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @xevent_channel  
 O tipo do Evento Estendido. O valor padrão é definido para retornar todos os eventos registrados para os 30 minutos anteriores. Os eventos registrados dependem do tipo de Eventos Estendidos habilitados. Você pode usar esse parâmetro para filtrar o procedimento armazenado para mostrar apenas eventos de um determinado tipo. Você pode especificar o nome completo do evento ou especifique uma subcadeia de caracteres, como: **'Admin'**, **'Analytic'**, **'Operational'**, e **'Debug'** . O @event_channel está **VARCHAR (255)**.  
  
 Para obter uma lista de tipos ativados no momento de evento, use o **managed_backup.fn_get_current_xevent_settings** função.  
  
 [@begin_time  
 O início do período dos eventos que devem ser exibidos. O @begin_time parâmetro é DATETIME com um valor padrão de NULL. Se isso não for especificado, os eventos dos últimos 30 minutos são exibidos.  
  
 @end_time  
 O fim do período dos eventos que devem ser exibidos. O @end_time parâmetro é DATATIME com um valor padrão de NULL.  Se isso não for especificado, os eventos até o horário atual são exibidos.  
  
## <a name="table-returned"></a>Tabela retornada  
 Esse procedimento armazenado retorna uma tabela com as seguintes informações:  
  
||||  
|-|-|-|  
|Nome da coluna|Tipo de dados|Description|  
|event_type|NVARCHAR(512)|Tipo de Evento Estendido.|  
|Evento|NVARCHAR(512)|Resumo dos logs de eventos.|  
|Timestamp|timestamp|Carimbo de data/hora de evento que mostra quando o evento foi gerado.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer **EXECUTE** permissões no procedimento armazenado. Ela também exige **VIEW SERVER STATE** permissões, pois chama internamente outros objetos do sistema que exigem essa permissão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os eventos registrados para os últimos 30 minutos  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics  
  
```  
  
 O exemplo a seguir retorna todos os eventos registrados para um intervalo específico.  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Admin',  
  @begin_time = '2013-06-01', @end_time = '2013-06-10'  
  
```  
  
 O exemplo a seguir retorna todos os eventos analíticos registrados para os últimos 30 minutos  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Analytic'  
  
```  
  
  
