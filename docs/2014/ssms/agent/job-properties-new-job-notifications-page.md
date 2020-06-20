---
title: 'Propriedades do trabalho: novo trabalho (página notificações) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: stevestein
ms.author: sstein
ms.openlocfilehash: b8fafac7faaf98fd8cf9bd3b0bf772dc77324bae
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062276"
---
# <a name="job-properties-new-job-notifications-page"></a>Propriedades do Trabalho: Novo Trabalho (página Notificações)
  Use esta página para definir ações para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executar quando o trabalho for concluído.  
  
## <a name="options"></a>Opções  
 **Mensagens**  
 Selecione esta opção para enviar email quando o trabalho terminar. Após selecionar essa opção, escolha o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Página**  
 Selecione esta opção para enviar email ao pager de um operador quando o trabalho terminar. Após selecionar essa opção, especifique o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Net send**  
 Selecione esta opção para usar o net send para notificar um operador quando o trabalho terminar. Após selecionar essa opção, especifique o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Gravar no log de eventos de Aplicativo do Windows**  
 Selecione esta opção para gravar uma entrada no log de eventos de aplicativo quando o trabalho terminar. Após selecionar essa opção, especifique a condição que fará com que a entrada seja gravada: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Excluir trabalho automaticamente**  
 Selecione essa opção para excluir o trabalho quando ele terminar. Após selecionar essa opção, especifique a condição que disparará a exclusão do trabalho: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar trabalhos](implement-jobs.md)   
 [Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
