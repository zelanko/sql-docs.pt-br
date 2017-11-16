---
title: "Propriedades do trabalho – Novo trabalho (página Notificações) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66811c4317cb975db74329d4dda7680d41ecb2ac
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="job-properties---new-job-notifications-page"></a>Propriedades do trabalho – Novo trabalho (página Notificações)
Use esta página para definir ações para que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent seja executado quando o trabalho terminar.  
  
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
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
[Como configurar o SQL Server Agent Mail para usar o Database Mail (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
