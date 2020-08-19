---
description: Classe de evento PreConnect:Starting
title: Classe de evento PreConnect:Starting | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: abc7be1a65c73d0a5651feb300672cc89460c162
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88384542"
---
# <a name="preconnectstarting-event-class"></a>Classe de evento PreConnect:Starting
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  A classe de evento PreConnect:Starting indica quando um gatilho LOGON ou a função classificador do Administrador de Recursos inicia a execução.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>Colunas de dados da classe de evento PreConnect:Starting  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|Não|  
|SPID|**int**|O ID de processo de servidor que dispara este evento.|12|Sim|  
|EventSubClass|**int**|1 para a função de classificador definida pelo usuário.|21|Sim|  
|StartTime|**datetime**|A hora que inicia a função de classificador definida pelo usuário.|14|Sim|  
|ObjectID|**int**|A ID do objeto do classificador definido pelo usuário.|22|Sim|  
|ObjectName|**nvarchar(256)**|O nome de duas partes da função de classificador definida pelo usuário. Por exemplo, dbo.classifier.|34|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [Classe de evento PreConnect:Completed](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
