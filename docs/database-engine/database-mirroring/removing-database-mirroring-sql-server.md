---
title: "Removendo o espelhamento de banco de dados (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "espelhamento de banco de dados [SQL Server], removendo"
  - "parando o espelhamento de banco de dados [SQL Server]"
  - "removendo o espelhamento de banco de dados [SQL Server]"
ms.assetid: 40c72091-8f03-4037-8b55-5e95309fe145
caps.latest.revision: 32
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 31
---
# Removendo o espelhamento de banco de dados (SQL Server)
  O proprietário do banco de dados pode interromper manualmente uma sessão de espelhamento de banco de dados a qualquer momento, em qualquer parceiro.  
  
## Impacto da remoção do espelhamento  
 Quando o espelhamento é removido, acontece o seguinte:  
  
-   A relação entre os parceiros e entre cada parceiro e a testemunha se rompe permanentemente, caso exista alguma relação.  
  
     Se os parceiros estiverem se comunicando entre si quando a sessão for interrompida, sua relação será imediatamente rompida em ambos os computadores. Se os parceiros não estiverem se comunicando (o banco de dados estiver em um estado DISCONNECTED no momento da interrupção), a relação será imediatamente interrompida no parceiro em que o espelhamento é interrompido; quando o outro parceiro tenta se reconectar, descobre que a sessão de espelhamento de banco de dados foi concluída.  
  
-   As informações sobre a sessão de espelhamento são descartadas, diferentemente de quando uma sessão é pausada. O espelhamento é removido do banco de dados principal e do banco de dados espelho. No **sys.databases**, a coluna **mirroring_state** e todas as demais colunas de espelhamento são definidas como NULL. Para obter mais informações, veja [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md).  
  
-   Cada instância de servidor parceiro é deixada com uma cópia separada do banco de dados.  
  
-   O banco de dados espelho é deixado em estado RESTORING (consulte a coluna **estado** do **sys.databases**), porque o banco de dados espelho foi criado usando RESTORE WITH NORECOVERY. Nesse momento, você pode descartar o banco de dados espelho anterior ou restaurá-lo usando WITH RECOVERY. Ao ser recuperado, o banco de dados diverge do banco de dados principal anterior porque a recuperação inicia uma nova bifurcação da recuperação.  
  
> [!NOTE]  
>  Para continuar o espelhamento depois de interromper uma sessão, é preciso estabelecer uma nova sessão de espelhamento de banco de dados. Se você criar um backup de log depois de ter interrompido um espelhamento, deverá registrá-lo no banco de dados espelho antes reiniciar o espelhamento.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para remover o espelhamento de banco de dados**  
  
-   [Remover o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
 **Para inicializar o espelhamento de banco de dados**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
 ![Ícone de seta usado com o link Voltar ao Início](../../analysis-services/instances/media/uparrow16x16.png "Ícone de seta usado com o link Voltar ao Início") [&#91;Início&#93;](#Top)  
  
## Consulte também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Pausando e retomando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  