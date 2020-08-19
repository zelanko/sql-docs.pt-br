---
description: Atualizar Monitor de Atividade do Trabalho
title: Atualização do Monitor de Atividade do Trabalho | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.jobactivitymon.refresh.f1
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 78141d10b6244308f075e420f1d1ea3501830286
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424038"
---
# <a name="job-activity-monitor-refresh"></a>Atualizar Monitor de Atividade do Trabalho
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use a caixa de diálogo **Atualizar Configurações** para configurar com que frequência o Monitor de Atividade do Trabalho obtém informações novas sobre a atividade de servidor. O Monitor de Atividade do Trabalho deve executar consultas no servidor monitorado para obter informações para a grade do Monitor de Atividade do Trabalho. Quando o intervalo de atualização automática for definido como menos de 30 segundos, o tempo usado para executar essas consultas poderá afetar o desempenho do servidor.  
  
 Para abrir essa caixa de diálogo, clique em **Exibir configurações de atualização**, na seção **Status** do Monitor de Atividade do Trabalho.  
  
## <a name="options"></a>Opções  
 **Atualizar automaticamente a cada**  
 Marque para iniciar a atualização automática de informações do Monitor de Atividade. Isso está definido como desativado por padrão.  
  
 **segundos**  
 O número de segundos entre as tentativas de atualização automática. O padrão é 60 segundos. Faz atualizações a cada 5 segundos quando definido como 5 ou menos.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar Atividade do Trabalho](../../ssms/agent/monitor-job-activity.md)  
  
  
