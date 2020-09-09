---
description: sys. time_zone_info (Transact-SQL)
title: sys. time_zone_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.time_zone_info
- sys.time_zone_info_TSQL
- time_zone_info
- time_zone_info_TSQL
helpviewer_keywords:
- sys.time_zone_info system table
ms.assetid: 3f51a9a4-75f8-4a11-9552-8bf6118b68da
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 51f3fd600b3c2c78caf437e758ece03aa325d29a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544956"
---
# <a name="systime_zone_info-transact-sql"></a>sys. time_zone_info (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Retorna informações sobre os fusos horários com suporte. Todos os fusos horários instalados no computador são armazenados no seguinte hive do registro:  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do fuso horário no formato padrão do Windows. Por exemplo, **hora padrão CEN. Austrália** ou **horário padrão europeu central**.|  
|**current_utc_offset**|**nvarchar (12)**|Deslocamento atual para UTC. Por exemplo, **+ 01:00** ou **-07:00**.|  
|**is_currently_dst**|**bit**|True se estiver observando o horário de verão.|  
  
## <a name="see-also"></a>Consulte Também  
 [GETUTCDATE &#40;&#41;Transact-SQL ](../../t-sql/functions/getutcdate-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [Exibições do catálogo de configuração em todo o servidor &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  
