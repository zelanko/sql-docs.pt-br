---
title: Atualização do Monitor de Atividade do Trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.jobactivitymon.refresh.f1
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14e4e42f4f756a7a63f4c0dfa17845c606233148
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059048"
---
# <a name="job-activity-monitor-refresh"></a>Atualizar Monitor de Atividade do Trabalho
  Use a caixa de diálogo **Atualizar Configurações** para configurar com que frequência o Monitor de Atividade do Trabalho obtém informações novas sobre a atividade de servidor. O Monitor de Atividade do Trabalho deve executar consultas no servidor monitorado para obter informações para a grade do Monitor de Atividade do Trabalho. Quando o intervalo de atualização automática for definido como menos de 30 segundos, o tempo usado para executar essas consultas poderá afetar o desempenho do servidor.  
  
 Para abrir essa caixa de diálogo, clique em **Exibir configurações de atualização**, na seção **Status** do Monitor de Atividade do Trabalho.  
  
## <a name="options"></a>Opções  
 **Atualizar automaticamente a cada**  
 Marque para iniciar a atualização automática de informações do Monitor de Atividade. Isso está definido como desativado por padrão.  
  
 **segundos**  
 O número de segundos entre as tentativas de atualização automática. O padrão é 60 segundos. Faz atualizações a cada 5 segundos quando definido como 5 ou menos.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar Atividade do Trabalho](../../ssms/agent/monitor-job-activity.md)  
  
  
