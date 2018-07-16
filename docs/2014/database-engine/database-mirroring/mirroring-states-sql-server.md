---
title: Estados de espelhamento (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- PENDING_FAILOVER state
- mirroring states [SQL Server]
- DISCONNECTED state
- SYNCHRONIZING state
- SYNCHRONIZED state
- SUSPENDED state
- database mirroring [SQL Server], states
ms.assetid: 90062917-74f9-471b-b49e-bc153ae1a468
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 10cc3385d0bbcd7832533e1e375401b1b060c959
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320716"
---
# <a name="mirroring-states-sql-server"></a>Estados de espelhamento (SQL Server)
  Durante uma sessão de espelhamento de banco de dados, o banco de dados espelho está sempre em um estado específico (o *estado de espelhamento*). O estado do banco de dados reflete o status de comunicação, o fluxo de dados e a diferença nos dados entre os parceiros. A sessão de espelhamento de banco de dados adota o mesmo estado que o banco de dados principal.  
  
 Ao longo de uma sessão de espelhamento de banco de dados, as instâncias de servidor monitoram umas às outras. Os parceiros usam o estado de espelhamento para monitorar o banco de dados. Com exceção do estado PENDING_FAILOVER, os bancos de dados principal e espelho estão sempre no mesmo estado. Se uma testemunha for definida para a sessão, cada parceiro monitorará a testemunha que usar seu estado de conexão (CONNECTED ou DISCONNECTED).  
  
 Os estados possíveis de espelhamento de banco de dados são:  
  
|estado de espelhamento|Description|  
|---------------------|-----------------|  
|SYNCHRONIZING|O conteúdo do banco de dados espelho está ficando atrás do conteúdo do banco de dados principal. O servidor principal está enviando registros de log para o servidor espelho, que está aplicando as alterações ao banco de dados espelho para rolá-lo adiante.<br /><br /> No início de uma sessão de espelhamento de banco de dados, o banco de dados está no estado SYNCHRONIZING. O servidor principal está servindo o banco de dados e o espelho está tentando manter-se atualizado.|  
|SYNCHRONIZED|Quando o servidor espelho torna-se suficientemente atualizado com relação ao servidor principal, o estado de espelhamento muda para SYNCHRONIZED. O banco de dados permanece nesse estado enquanto o servidor principal continua enviando alterações para o servidor espelho e o servidor espelho continua aplicando as alterações ao banco de dados espelho.<br /><br /> Se a segurança da transação for definida como FULL, suporte ao failover automático e ao failover manual no estado SYNCHRONIZED, não haverá perda de dados após um failover.<br /><br /> Se a segurança da transação for off, sempre será possível alguma perda de dados, mesmo no estado SYNCHRONIZED.|  
|SUSPENDED|A cópia espelhada do banco de dados não está disponível. O banco de dados principal está sendo executado sem enviar nenhum log ao servidor espelho, uma condição conhecida como *execução exposta*. Esse é o estado após um failover.<br /><br /> Uma sessão também pode se tornar SUSPENDED como resultado de erros de reversão ou se o administrador pausar a sessão.<br /><br /> SUSPENDED é um estado persistente que sobrevive a desligamentos e inicializações do parceiro.|  
|PENDING_FAILOVER|Esse estado é encontrado apenas no servidor principal após um failover ter começado, mas o servidor não tiver feito a transição para a função espelho.<br /><br /> Quando o failover é iniciado, o banco de dados principal vai para o estado PENDING_FAILOVER, termina rapidamente quaisquer conexões de usuário e assume em seguida a função espelho.|  
|DISCONNECTED|O parceiro perdeu comunicação com o outro parceiro.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
