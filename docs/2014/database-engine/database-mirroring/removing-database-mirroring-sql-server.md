---
title: Removendo o espelhamento de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- stopping database mirroring [SQL Server]
- removing database mirroring [SQL Server]
ms.assetid: 40c72091-8f03-4037-8b55-5e95309fe145
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 414cdedb8f2bc3dee4edc792c11b6438306818c6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088016"
---
# <a name="removing-database-mirroring-sql-server"></a>Removendo o espelhamento de banco de dados (SQL Server)
  O proprietário do banco de dados pode interromper manualmente uma sessão de espelhamento de banco de dados a qualquer momento, em qualquer parceiro.  
  
## <a name="impact-of-removing-mirroring"></a>Impacto da remoção do espelhamento  
 Quando o espelhamento é removido, acontece o seguinte:  
  
-   A relação entre os parceiros e entre cada parceiro e a testemunha se rompe permanentemente, caso exista alguma relação.  
  
     Se os parceiros estiverem se comunicando entre si quando a sessão for interrompida, sua relação será imediatamente rompida em ambos os computadores. Se os parceiros não estiverem se comunicando (o banco de dados estiver em um estado DISCONNECTED no momento da interrupção), a relação será imediatamente interrompida no parceiro em que o espelhamento é interrompido; quando o outro parceiro tenta se reconectar, descobre que a sessão de espelhamento de banco de dados foi concluída.  
  
-   As informações sobre a sessão de espelhamento são descartadas, diferentemente de quando uma sessão é pausada. O espelhamento é removido do banco de dados principal e do banco de dados espelho. No **sys.databases**, a coluna **mirroring_state** e todas as demais colunas de espelhamento são definidas como NULL. Para obter mais informações, veja [sys.database_mirroring &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql).  
  
-   Cada instância de servidor parceiro é deixada com uma cópia separada do banco de dados.  
  
-   O banco de dados espelho é deixado em estado RESTORING (consulte a coluna **estado** do **sys.databases**), porque o banco de dados espelho foi criado usando RESTORE WITH NORECOVERY. Nesse momento, você pode descartar o banco de dados espelho anterior ou restaurá-lo usando WITH RECOVERY. Ao ser recuperado, o banco de dados diverge do banco de dados principal anterior porque a recuperação inicia uma nova bifurcação da recuperação.  
  
> [!NOTE]  
>  Para continuar o espelhamento depois de interromper uma sessão, é preciso estabelecer uma nova sessão de espelhamento de banco de dados. Se você criar um backup de log depois de ter interrompido um espelhamento, deverá registrá-lo no banco de dados espelho antes reiniciar o espelhamento.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para remover o espelhamento de banco de dados**  
  
-   [Remover o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
 **Para inicializar o espelhamento de banco de dados**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  

  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Pausando e retomando o espelhamento de banco de dados &#40;SQL Server&#41;](pausing-and-resuming-database-mirroring-sql-server.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
