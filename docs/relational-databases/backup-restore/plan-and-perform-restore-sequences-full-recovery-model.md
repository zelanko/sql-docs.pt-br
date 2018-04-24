---
title: Planejar e executar sequências de restauração (modelo de recuperação completa) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- restore sequences [SQL Server], planning for
- full recovery model [SQL Server], planning restore sequences
ms.assetid: 9cbefaf8-d2b6-41c9-83fc-b3807a841fe2
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79425550a136d26f5b135e4691f9a35efe56f5b4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="plan-and-perform-restore-sequences-full-recovery-model"></a>Planejar e executar sequências de restauração (modelo de recuperação completa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico explica como planejar e executar uma sequência de restauração para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que normalmente usam o modelo de recuperação completa. Uma *sequência de restauração* é uma sequência de uma ou mais instruções [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) . Geralmente, uma sequência de restauração inicializa os conteúdos do banco de dados, arquivos, e/ou páginas sendo restaurados (a fase de cópia de dados), efetua roll forward das transações registradas (a fase refazer) e reverte as transações não confirmadas (a fase desfazer).  
  
 Em casos simples, uma sequência de restauração requer apenas um backup de banco de dados completo, um backup de banco de dados diferencial e os backups de log subsequentes. Nesses casos, criar uma sequência de restauração correta é fácil. Por exemplo, para restaurar todo um banco de dados para o ponto de uma falha, comece fazendo backup do log de transações ativo (a *parte final* do log). Depois, restaure o backup de banco de dados completo mais recente, o backup diferencial mais recente (se houver) e todos os backups de log subsequentes na ordem em que foram feitos.  
  
 Em casos mais complexos, criar uma sequência de restauração correta pode ser um processo complexo. Por exemplo, uma sequência de restauração pode exigir vários backups de arquivo ou restauração de dados a um point-in-time específico. Em casos muito complexos, você pode ter que transpor um caminho de recuperação que abrange uma ou mais bifurcações de recuperação.  
  
> [!NOTE]  
>  Um *caminho de recuperação* é a sequência de backups de dados e logs que levou o banco de dados até um momento específico (conhecido como um ponto de recuperação). Um caminho de recuperação é um conjunto específico de transformações que levaram à evolução do banco de dados, mas mantiveram a sua consistência. Um caminho de recuperação descreve um intervalo de LSNs de um ponto inicial (LSN,GUID) até um ponto final (LSN,GUID). O intervalo de LSNs em um caminho de recuperação pode percorrer uma ou mais ramificações de recuperação, do início ao fim.  
  
## <a name="to-plan-a-restore-sequence"></a>Para planejar uma sequência de restauração  
 Antes de iniciar uma sequência de restauração, siga estas etapas:  
  
1.  Crie um backup do final do log do banco de dados, se puder. Para obter mais informações, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
2.  Determine o ponto de recuperação desejado.  
  
     O ponto de recuperação desejado pode ser qualquer point-in-time ou marca em um backup de log de transações. Para obter mais informações, veja [Restaurar um Banco de Dados SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md) ou [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
3.  Determine o tipo de restauração que você deseja executar. Para obter mais informações, veja [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
4.  Identifique quais backups são necessários e certifique-se de que os conjuntos de mídia e dispositivos de backup necessários estão disponíveis. Para obter mais informações, veja [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md) e [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
## <a name="to-perform-a-restore-sequence"></a>Para executar uma sequência de restauração  
 Para executar uma sequência de restauração, siga estes passos:  
  
1.  Para iniciar a sequência, restaure um ou mais backups de dados, como: um backup de banco de dados, um backup parcial, ou um ou mais backups de arquivo.  
  
2.  Opcionalmente, restaure os últimos backups diferenciais baseados nestes backups completos.  
  
     Para cada backup completo que você planeja restaurar, determine se ele é a base de qualquer backup diferencial. Nesse caso, restaure o backup diferencial mais recente, se puder. Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
3.  Efetue roll forward do banco de dados restaurando backups de log em sequência, terminando com o backup que contém o ponto de recuperação. A aplicação de todos os backups de log depende se o backup de log contém o ponto de recuperação desejado, como segue:  
  
    -   Se o ponto de recuperação for o ponto de falha, você deve restaurar todo backup de log criado desde o último backup de dados (completo ou diferencial) restaurado. Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
    -   Para a restauração point-in-time, podem não ser necessários os backups de log mais recentes. Se você usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o orientador de recuperação de banco de dados garantirá que apenas os backups necessários para restaurar até o ponto especificado sejam selecionados. Esses backups compõem o plano de restauração recomendado para a sua restauração pontual. Para obter mais informações, veja [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
## <a name="restarting-a-restore-sequence"></a>Reinicializando uma sequência de restauração  
 Se você encontrar um problema com o resultado de uma sequência de restauração, pode encerrá-la e reiniciar a sequência de restauração desde o início. Por exemplo, se você restaurar muitos backups de log acidentalmente e exceder o ponto de recuperação pretendido, reinicialize a sequência de restauração até o backup de log que contém o ponto de recuperação desejado.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
