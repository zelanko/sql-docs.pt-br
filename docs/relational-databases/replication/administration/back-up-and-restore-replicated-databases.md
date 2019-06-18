---
title: Fazer backup e restaurar bancos de dados replicados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication]
- administering replication, restoring
- backing up replicated databases
- backups [SQL Server replication], about backups
- restoring replicated databases [SQL Server replication]
- recovery [SQL Server replication], about recovery
- restoring databases [SQL Server], replicated databases
- backing up databases [SQL Server], replicated databases
- restoring [SQL Server replication], about restoring
- recovery [SQL Server replication]
- replication [SQL Server], administering
- distribution databases [SQL Server replication], backing up
- restoring [SQL Server replication]
- administering replication, backing up
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b583be423e6f70fa23ae105082fe0b39f221072f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62665098"
---
# <a name="back-up-and-restore-replicated-databases"></a>Fazer backup e restaurar bancos de dados replicados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Bancos de dados replicados requerem atenção especial em relação a backup e restauração de dados. Este tópico fornece informações iniciais e links para obter mais informações sobre estratégias de backup e restauração para cada tipo de replicação.  
  
 A replicação oferece suporte à restauração de bancos de dados replicados para o mesmo servidor e banco de dados dos quais o backup foi criado. Se você restaurar um backup de um banco de dados replicado para outro servidor ou banco de dados, as configurações de replicação não poderão ser preservadas. Neste caso, você deve recriar todas as publicações e assinaturas depois que os backups forem restaurados.  
  
> [!NOTE]  
>  Será possível restaurar um banco de dados replicado para um servidor auxiliar se estiver sendo usada a remessa de log. Para obter mais informações, veja [Replicação e envio de logs &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 Deve ser feito backup regularmente para bancos de dados replicados e bancos de dados do sistema associados. Faça backup dos seguintes bancos de dados:  
  
-   O banco de dados de publicação no Publicador.  
  
-   O banco de dados de distribuição no Distribuidor.  
  
-   O banco de dados de assinatura em cada Assinante.  
  
-   Os bancos de dados de sistema **mestre** e **msdb** no Publicador, Distribuidor e todos os Assinantes. Esses bancos de dados devem ter, cada um, seus backups realizados em simultâneo com o banco de dados de replicação relevante. Por exemplo, faça o backup dos bancos de dados **mestre** e **msdb** no Publicador ao mesmo tempo em que executa o backup do banco de dados de publicação. Se o banco de dados de publicação for restaurado, assegure-se de que os bancos de dados **mestre** e **msdb** são consistentes com o banco de dados de publicação, em termos de configuração de replicação e ajustes.  
  
 Se você executar backups de log regulares, qualquer alteração relacionada à replicação deverá ser capturada nos backups de log. Se não executar backups de log, um backup deve ser executado sempre que uma configuração pertinente à replicação for alterada. Para obter mais informações, consulte [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## <a name="backup-and-restore-strategies"></a>Estratégias de backup e restauração  
 As estratégias de backup e restauração de cada nó em uma topologia de replicação diferem de acordo com tipo de replicação usado. Para obter informações sobre estratégias de backup e restauração para cada tipo de replicação, consulte os tópicos abaixo:  
  
-   [Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [Estratégias para fazer backup e restaurar a replicação de mesclagem](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 Como parte de qualquer estratégia de recuperação, mantenha sempre um script atual de suas configurações de replicação em um local seguro. No caso de uma falha do servidor ou da necessidade de configurar um ambiente de teste, você poderá modificar o script alterando as referências no nome do servidor e isso poderá ser usado para ajudar a recriar suas configurações de replicação. Além de executar o script em suas configurações de replicação atuais, você deve executar o script de habilitação e desabilitação da replicação. Para obter informações sobre a execução do script de objetos de replicação, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Fazer backup e restaurar bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
