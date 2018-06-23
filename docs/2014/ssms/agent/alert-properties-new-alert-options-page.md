---
title: 'Propriedades do alerta: Novo alerta (página Opções) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b5e65400a2b7f82316ecdae3f92d34e40ac0715e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008825"
---
# <a name="alert-properties-new-alert-options-page"></a>Propriedades do alerta: Novo alerta (página Opções)
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
  
  