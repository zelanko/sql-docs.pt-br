---
title: Pausando e retomando o espelhamento de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- sessions [SQL Server], database mirroring
- resuming database mirroring
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: c67802c6-ee8c-4cbd-a6d4-f7b80413a4ab
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 3f9506f97af3f1a276efef01f4c77d2b86f6a7de
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795337"
---
# <a name="pausing-and-resuming-database-mirroring-sql-server"></a>Pausando e retomando o espelhamento de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O proprietário de banco de dados pode pausar e depois retomar uma sessão de espelhamento de banco de dados a qualquer hora. Pausar preserva o estado de sessão enquanto suspende o espelhamento. Durante o gargalo, pausar pode ser útil para melhorar o desempenho no servidor principal.  
  
 Quando uma sessão é pausada, o banco de dados principal permanece disponível. Pausar define o estado da sessão de espelhamento para SUSPENDED e o banco de dados espelho já não mantém o ritmo do banco de dados principal, fazendo o banco de dados principal executar exposto.  
  
 Nós recomendamos que você continue uma sessão pausada rapidamente, pois, contanto que uma sessão de espelhamento de banco de dados permaneça pausada, o log de transações não pode ser truncado. Então, se uma sessão de espelhamento de banco de dados for pausada por muito tempo, o log de transações é preenchido, tornando o banco de dados indisponível. Para uma explicação do por que isto acontece, consulte "Como pausar e continuar afetam o truncamento de log ", a seguir neste tópico.  
  
> [!IMPORTANT]  
>  Após um serviço forçado, quando o servidor principal original é reconectado, o espelhamento é suspenso. A retomada do espelhamento nessa situação pode causar perda de dados no servidor principal original. Para obter informações sobre como gerenciar possível perda de dados, consulte [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 **Neste tópico:**  
  
-   [Como pausar e continuar afetam o truncamento de log](#EffectOnLogTrunc)  
  
-   [Evitar um log de transações completo](#AvoidFullLog)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="EffectOnLogTrunc"></a> Como pausar e continuar afetam o truncamento de log  
 Normalmente, quando um ponto de verificação automático é executado em um banco de dados, seu log de transações é truncado àquele ponto de verificação após o próximo backup de log. Enquanto uma sessão de espelhamento de banco de dados permanece pausada, tudo nos registros de log atuais permanece ativo porque o servidor principal está esperando para enviá-los ao servidor espelho. Os registros de log não enviados acumulam no log de transações do banco de dados principal até que a sessão continue e o servidor principal envie os registros de log ao servidor espelho.  
  
 Quando a sessão é reiniciada, o servidor principal começa imediatamente a enviar os registros de log acumulados ao servidor espelho. Depois que o servidor espelho confirme que colocou em fila o registro de log que corresponde ao ponto de verificação automático mais antigo, o servidor principal trunca o log do banco de dados principal àquele ponto de verificação. O servidor espelho trunca a fila de restauração no mesmo registro de log. Como este processo é repetido para cada ponto de verificação sucessivo, o log é truncado nos estágios, ponto de verificação por ponto de verificação.  
  
> [!NOTE]  
>  Para obter mais informações sobre pontos de verificação e truncamento de log, veja [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
##  <a name="AvoidFullLog"></a> Evitar um log de transações completo  
 Se o log completar (ou porque alcança seu tamanho máximo ou a instância de servidor executa fora de espaço), o banco de dados não poderá mais executar quaisquer atualizações. Para evitar este problema, há duas alternativas:  
  
-   Continue a sessão de espelhamento de banco de dados antes que o log se complete ou adicione mais espaço de log. Continuar o espelhamento de banco de dados permite ao servidor principal enviar seu log ativo acumulado ao servidor espelho e põe o banco de dados espelho no estado SYNCHRONIZING. O servidor espelho pode então endurecer o log no disco e começar a refazê-lo.  
  
-   Pare a sessão de espelhamento de banco de dados removendo o espelhamento.  
  
     Diferente de pausar a sessão, remover o espelhamento descarta todas as informações sobre a sessão de espelhamento. Cada instância de servidor parceiro mantém sua própria cópia do banco de dados. Se a cópia de espelho anterior for recuperada, ela divergirá da cópia principal anterior e ficará atrasada pelo tempo decorrido desde o inicio da pausa da sessão. Para obter mais informações, veja [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para pausar ou retomar o espelhamento de banco de dados**  
  
-   [Pausar ou retomar uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
 **Para parar o espelhamento de banco de dados.**  
  
-   [Remover o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
  
