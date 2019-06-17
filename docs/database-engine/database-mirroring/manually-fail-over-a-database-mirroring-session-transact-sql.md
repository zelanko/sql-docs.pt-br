---
title: Fazer failover manual de uma sessão de espelhamento de banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: cff69cccd05d48df6affeca17a6799f82e26e1f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795395"
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
  
  
