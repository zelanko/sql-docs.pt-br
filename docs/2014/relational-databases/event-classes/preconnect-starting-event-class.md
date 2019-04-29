---
title: Classe de evento PreConnect:Starting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0986e654430a47cc494bf1646c222b4888fc105b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63033508"
---
# <a name="preconnectstarting-event-class"></a>Classe de evento PreConnect:Starting
  A classe de evento PreConnect:Starting indica quando um gatilho LOGON ou a função classificador do Administrador de Recursos inicia a execução.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>Colunas de dados da classe de evento PreConnect:Starting  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|215|27|Não|  
|SPID|`int`|O ID de processo de servidor que dispara este evento.|12|Sim|  
|EventSubClass|`int`|1 para a função de classificador definida pelo usuário.|21|Sim|  
|StartTime|`datetime`|A hora que inicia a função de classificador definida pelo usuário.|14|Sim|  
|ObjectID|`int`|A ID do objeto do classificador definido pelo usuário.|22|Sim|  
|ObjectName|`nvarchar(256)`|O nome de duas partes da função de classificador definida pelo usuário. Por exemplo, dbo.classifier.|34|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [Classe de evento PreConnect:Completed](preconnect-completed-event-class.md)   
 [Resource Governor](../resource-governor/resource-governor.md)  
  
  
