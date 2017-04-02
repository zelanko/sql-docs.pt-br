---
title: "Atualizar Monitor de Atividade do Trabalho | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.jobactivitymon.refresh.f1"
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Atualizar Monitor de Atividade do Trabalho
  Use a caixa de diálogo **Atualizar Configurações** para configurar com que frequência o Monitor de Atividade do Trabalho obtém informações novas sobre a atividade de servidor. O Monitor de Atividade do Trabalho deve executar consultas no servidor monitorado para obter informações para a grade do Monitor de Atividade do Trabalho. Quando o intervalo de atualização automática for definido como menos de 30 segundos, o tempo usado para executar essas consultas poderá afetar o desempenho do servidor.  
  
 Para abrir essa caixa de diálogo, clique em **Exibir configurações de atualização**, na seção **Status** do Monitor de Atividade do Trabalho.  
  
## Opções  
 **Atualizar automaticamente a cada**  
 Marque para iniciar a atualização automática de informações do Monitor de Atividade. Isso está definido como desativado por padrão.  
  
 **segundos**  
 O número de segundos entre as tentativas de atualização automática. O padrão é 60 segundos. Faz atualizações a cada 5 segundos quando definido como 5 ou menos.  
  
## Consulte também  
 [Monitorar Atividade do Trabalho](../../ssms/agent/monitor-job-activity.md)  
  
  