---
title: Sondar servidores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 740bac0995d53c324c88d780c4d19c583713c136
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="poll-servers"></a>Sondar servidores
Quando é implementada administração multisservidor, os servidores de destino contatam periodicamente o servidor mestre para carregar informações sobre trabalhos executados e baixar novos trabalhos. O processo de contatar o servidor mestre é chamado de *sondagem de servidor* , que acontece em *intervalos de sondagem*regulares.  
  
## <a name="polling-intervals"></a>Intervalos de sondagem  
O intervalo de sondagem (um minuto, por padrão) controla a frequência com que o servidor de destino se conecta ao servidor mestre para baixar instruções e carregar os resultados da execução de trabalhos.  
  
Quando um servidor de destino sonda o servidor mestre, ele lê as operações atribuídas a si na tabela **sysdownloadlist** do banco de dados **msdb** . Essas operações controlam trabalhos multisservidor e diversos aspectos do comportamento de um servidor de destino. São exemplos dessas operações a exclusão, inserção ou início de um trabalho e a atualização do intervalo de sondagem de um servidor de destino.  
  
As operações são postadas na tabela **sysdownloadlist** , de um destes modos:  
  
-   Explicitamente, usando o procedimento armazenado **sp_post_msx_operation** .  
  
-   Implicitamente, usando outros procedimentos armazenados de trabalho.  
  
Se usar procedimentos armazenados de trabalho para modificar agendas ou etapas de trabalho multisservidor ou se usar o SQL Distributed Management Objects (SQL-DMO) para controlar trabalhos multisservidor, emita o seguinte comando após efetuar as modificações nas agendas ou etapas de trabalho:  
  
```  
EXECUTE msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Emitir este comando mantém os servidores de destino sincronizados com a definição de trabalho atual.  
  
Você não terá que postar operações explicitamente se usar o seguinte:  
  
-   O Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] , para controlar trabalhos multisservidor.  
  
-   Procedimentos armazenados de trabalho que não modificam agendas nem etapas de trabalho.  
  
**Para forçar um servidor de destino a sondar o servidor mestre**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>Consulte também  
[Gerenciar eventos](../../ssms/agent/manage-events.md)  
  

