---
title: 'Propriedades do trabalho: Novo trabalho (página notificações) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 170456c9aeacb804a02d0e7450647b67453e635f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196766"
---
# <a name="job-properties-new-job-notifications-page"></a>Propriedades do trabalho: Novo trabalho (página notificações)
  Use esta página para definir ações para que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seja executado quando o trabalho terminar.  
  
## <a name="options"></a>Opções  
 **Email**  
 Selecione esta opção para enviar email quando o trabalho terminar. Após selecionar essa opção, escolha o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Página**  
 Selecione esta opção para enviar email ao pager de um operador quando o trabalho terminar. Após selecionar essa opção, especifique o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Net send**  
 Selecione esta opção para usar o net send para notificar um operador quando o trabalho terminar. Após selecionar essa opção, especifique o operador a ser notificado, além das condições que dispararão a notificação: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Gravar no log de eventos de Aplicativo do Windows**  
 Selecione esta opção para gravar uma entrada no log de eventos de aplicativo quando o trabalho terminar. Após selecionar essa opção, especifique a condição que fará com que a entrada seja gravada: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
 **Excluir trabalho automaticamente**  
 Selecione essa opção para excluir o trabalho quando ele terminar. Após selecionar essa opção, especifique a condição que disparará a exclusão do trabalho: **Quando o trabalho for bem-sucedido**; **Quando ocorrer falha no trabalho**; ou **Quando o trabalho for concluído**.  
  
## <a name="see-also"></a>Consulte também  
 [Implementar trabalhos](implement-jobs.md)   
 [Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
