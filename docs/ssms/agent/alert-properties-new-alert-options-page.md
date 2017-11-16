---
title: "Propriedades do alerta – Novo alerta (página Opções) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b71cd3ba732cb48898fb4550c4476c8294307244
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="alert-properties---new-alert-options-page"></a>Propriedades do alerta – Novo alerta (página Opções)
Use essa página para exibir e modificar opções para os alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Email**  
Inclua texto de erro do evento, se houver, em notificações de email.  
  
**Pager**  
Inclua texto de erro do evento, se houver, em notificações de pager.  
  
**Net send**  
Inclua texto de erro do evento, se houver, em notificações enviadas pela net.  
  
**Mensagem de notificação adicional para enviar**  
Digite qualquer texto adicional para incluir em mensagens de notificação.  
  
**Atraso entre as respostas**  
Especifique um intervalo para ocorrências repetidas do evento. Alguns eventos podem acontecer com frequência durante um curto intervalo de tempo. Nesse caso, você pode desejar saber que o evento ocorreu, mas talvez não queira uma resposta para cada evento. Use essa opção para especificar um tempo-limite. Com o intervalo, depois que o alerta responde a um evento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent espera pelo intervalo especificado antes de responder novamente, mesmo se o evento ocorrer durante o intervalo.  
  
**Minutes (minutos)**  
Especifique um intervalo em minutos. Para responder todas as vezes que o evento ocorrer, especifique 0 minuto e 0 segundo.  
  
**Seconds (segundos)**  
Especifique um intervalo em segundos. Para responder todas as vezes que o evento ocorrer, especifique 0 minuto e 0 segundo.  
  
## <a name="see-also"></a>Consulte também  
[Alertas](../../ssms/agent/alerts.md)  
  
