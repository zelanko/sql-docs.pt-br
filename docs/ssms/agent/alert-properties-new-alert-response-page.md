---
title: "Propriedades do alerta – Novo alerta (página Resposta) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb8013af5e072babcfe0936c08afb45c681331d1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="alert-properties---new-alert-response-page"></a>Propriedades do alerta – Novo alerta (página Resposta)
Use esta página para especificar um trabalho que você quer executar e para obter uma lista de operadores a serem notificados em resposta a um alerta do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Executar trabalho**  
Habilita as opções **Lista de trabalhos**, **Novo trabalho** e **Exibir trabalho** .  
  
**Novo trabalho**  
Abra a caixa de diálogo **Novo Trabalho** . Esse botão não está disponível quando **Executar trabalho** não está selecionado.  
  
**Exibir trabalho**  
Exiba ou modifique o trabalho selecionado. Essa opção não está disponível quando **Executar trabalho** não está selecionado.  
  
**Notificar operadores**  
Habilita os controles que permitem adicionar, remover ou alterar operadores.  
  
**Lista de operadores**  
Lista os operadores a notificar quando ocorrer um alerta. Para especificar um método de notificação, marque a caixa de seleção **Email**, **Pager**ou **Net send** que é exibida depois do nome do operador. Essa opção não está disponível quando **Notificar operadores** não está selecionado.  
  
**Email**  
Use email para notificar o operador.  
  
**Pager**  
Use o endereço de email do pager para notificar o operador.  
  
**Net send**  
Use **net send** para notificar o operador.  
  
**Novo operador**  
Exibe a caixa de diálogo **Novo Operador** que você pode usar para criar um operador novo.  
  
**Exibir operador**  
Exibe a caixa de diálogo **Propriedades** para o operador selecionado atualmente. Você pode exibir e modificar as propriedades do operador na caixa de diálogo **Propriedades do Operador** .  
  
## <a name="see-also"></a>Consulte também  
[Alertas](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[Alertas](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
  
