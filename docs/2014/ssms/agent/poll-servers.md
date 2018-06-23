---
title: Sondar servidores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: efb1c63e6fed68dff7425145aa89f2be1f79ae84
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120710"
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
  
-   O Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , para controlar trabalhos multisservidor.  
  
-   Procedimentos armazenados de trabalho que não modificam agendas nem etapas de trabalho.  
  
 **Para forçar um servidor de destino a sondar o servidor mestre**  
  
-   [SQL Server Management Studio](force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar eventos](manage-events.md)  
  
  
