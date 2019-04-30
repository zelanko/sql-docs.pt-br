---
title: 'Propriedades do Alerta: Novo alerta (página Opções) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 69f467af1c797b9bf1cfa55c7def8456ad4a32bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061255"
---
# <a name="alert-properties-new-alert-options-page"></a>Propriedades do Alerta: Novo Alerta (página Opções)
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
  
  
