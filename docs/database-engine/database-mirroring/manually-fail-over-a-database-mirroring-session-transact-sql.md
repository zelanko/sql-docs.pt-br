---
title: "Executar failover manualmente em uma sess&#227;o de espelhamento de banco de dados (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "failover [SQL Server], espelhamento de banco de dados"
  - "failover manual [SQL Server]"
  - "espelhamento de banco de dados [SQL Server], failover"
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
caps.latest.revision: 32
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 32
---
# Executar failover manualmente em uma sess&#227;o de espelhamento de banco de dados (Transact-SQL)
  Quando o banco de dados espelho for sincronizado (ou seja, quando o banco de dados estiver no estado SYNCHRONIZED), o proprietário do banco de dados poderá iniciar failover manual para o servidor espelho. O failover manual só pode ser iniciado do servidor principal.  
  
### Para efetuar manualmente o failover de uma sessão de espelhamento de banco de dados  
  
1.  Conecte-se ao servidor principal.  
  
2.  Defina o contexto do banco de dados como o banco de dados **mestre**:  
  
     **USE master;**  
  
3.  Emita a seguinte instrução no servidor principal:  
  
     [ALTER DATABASE](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md) *database_name* SET PARTNER FAILOVER, em que *database_name* é o banco de dados espelhado.  
  
     Isso inicia uma transição imediata do servidor espelho para a função principal.  
  
 No principal anterior, clientes são desconectados do banco de dados e são revertidos em transações de voo.  
  
> [!NOTE]  
>  As transações que forem preparadas usando o Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)], mas que ainda não estiverem confirmadas quando ocorrer um failover, serão consideradas anuladas depois da falha do banco de dados.  
  
## Consulte também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [Executar failover manualmente de uma sessão de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  