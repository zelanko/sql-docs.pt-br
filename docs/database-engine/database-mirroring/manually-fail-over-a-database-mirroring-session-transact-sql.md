---
title: Fazer failover manual de uma sessão de espelhamento de banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8f8c7b45498787e09e2ac28db76792dbf34f6f0f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="manually-fail-over-a-database-mirroring-session-transact-sql"></a>Executar failover manualmente em uma sessão de espelhamento de banco de dados (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando o banco de dados espelho for sincronizado (ou seja, quando o banco de dados estiver no estado SYNCHRONIZED), o proprietário do banco de dados poderá iniciar failover manual para o servidor espelho. O failover manual só pode ser iniciado do servidor principal.  
  
### <a name="to-manually-fail-over-a-database-mirroring-session"></a>Para efetuar manualmente o failover de uma sessão de espelhamento de banco de dados  
  
1.  Conecte-se ao servidor principal.  
  
2.  Defina o contexto do banco de dados como o banco de dados **mestre** :  
  
     **USE master;**  
  
3.  Emita a seguinte instrução no servidor principal:  
  
     [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md) *database_name* SET PARTNER FAILOVER, em que *database_name* é o banco de dados espelhado.  
  
     Isso inicia uma transição imediata do servidor espelho para a função principal.  
  
 No principal anterior, clientes são desconectados do banco de dados e são revertidos em transações de voo.  
  
> [!NOTE]  
>  As transações que forem preparadas usando o Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , mas que ainda não estiverem confirmadas quando ocorrer um failover, serão consideradas anuladas depois da falha do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Fazer failover manual de uma sessão de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  
