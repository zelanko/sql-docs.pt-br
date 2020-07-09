---
title: Fazer failover manual de um espelho de banco de dados para o parceiro
description: Instruções para fazer failover manual de um espelho de banco de dados principal para um parceiro secundário usando T-SQL (Transact-SQL).
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 34fdb80d9c1393b25a4cdbff63f0546ec6d9ddac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754600"
---
# <a name="manually-fail-over-a-database-mirroring-session-transact-sql"></a>Executar failover manualmente em uma sessão de espelhamento de banco de dados (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
  
