---
title: 'Propriedades do alerta: Novo alerta (página Opções) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59e5ac1f951ce897b058d224701d1a6936bfa11f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173306"
---
# <a name="alert-properties-new-alert-options-page"></a>Propriedades do alerta: novo alerta (página Opções)
  Use essa página para exibir e modificar opções para os alertas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
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
 Especifique um intervalo para ocorrências repetidas do evento. Alguns eventos podem acontecer com frequência durante um curto intervalo de tempo. Nesse caso, você pode desejar saber que o evento ocorreu, mas talvez não queira uma resposta para cada evento. Use essa opção para especificar um tempo-limite. Com o intervalo, depois que o alerta responde a um evento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent espera pelo intervalo especificado antes de responder novamente, mesmo se o evento ocorrer durante o intervalo.  
  
 **Minutes (minutos) (minutos)**  
 Especifique um intervalo em minutos. Para responder todas as vezes que o evento ocorrer, especifique 0 minuto e 0 segundo.  
  
 **Seconds (segundos) (segundos)**  
 Especifique um intervalo em segundos. Para responder todas as vezes que o evento ocorrer, especifique 0 minuto e 0 segundo.  
  
## <a name="see-also"></a>Consulte também  
 [Alertas](alerts.md)  
  
  
