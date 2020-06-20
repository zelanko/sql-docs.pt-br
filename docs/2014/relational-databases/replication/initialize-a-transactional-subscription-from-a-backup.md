---
title: Inicializar uma assinatura transacional de um backup (Programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1563d58f2d54f77680781e22a162112ade1658e4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057111"
---
# <a name="initialize-a-transactional-subscription-from-a-backup-replication-transact-sql-programming"></a>Inicializar uma assinatura transacional de um backup (Programação Transact-SQL de replicação)
  Embora uma assinatura a uma publicação transacional seja geralmente inicializada com um instantâneo, é possível inicializar uma assinatura de backup usando procedimentos de replicação armazenados. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>Para inicializar um assinante transacional a partir de backup  
  
1.  Para uma publicação existente, certifique-se de que a publicação dê suporte à capacidade de inicializar do backup, executando [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) no Publicador no banco de dados de publicação. Observe o valor de **allow_initialize_from_backup** no conjunto de resultados.  
  
    -   Se o valor for **1**, a publicação oferece suporte a essa funcionalidade.  
  
    -   Se o valor for **0**, execute [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **allow_initialize_from_backup** para ** \@ Propriedade** e um valor de `true` para ** \@ valor**.  
  
2.  Para uma nova publicação, execute [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de `true` para **allow_initialize_from_backup**. Para obter mais informações, consulte [criar uma publicação](publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Para evitar perder dados do assinante, ao usar **sp_addpublication** com `@allow_initialize_from_backup = N'true'`, sempre use `@immediate_sync = N'true'`.  
  
3.  Crie um backup do banco de dados de publicação usando a instrução [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
4.  Restaure o backup no Assinante usando a instrução [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
5.  No Publicador no banco de dados de publicação, execute o procedimento armazenado [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique os seguintes parâmetros:  
  
    -   ** \@ sync_type** -um valor de **inicializar com backup**.  
  
    -   ** \@ backupdevicetype** -o tipo de dispositivo de backup: **lógico** (padrão), **disco**ou **fita**.  
  
    -   ** \@ BackupDeviceName** -o dispositivo de backup lógico ou físico a ser usado para a restauração.  
  
         Para um dispositivo lógico, especifique o nome do dispositivo de backup especificado quando **sp_addumpdevice** foi usado para criar o dispositivo.  
  
         Para um dispositivo físico, especifique um caminho completo e nome de arquivo, como `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\BACKUP\Mybackup.dat'` ou `TAPE = '\\.\TAPE0'`.  
  
    -   Adicional ** \@ senha** -uma senha que foi fornecida quando o conjunto de backup foi criado.  
  
    -   Adicional ** \@ MEDIAPASSWORD** -uma senha que foi fornecida quando o conjunto de mídias foi formatado.  
  
    -   Adicional ** \@ fileidhint** -identificador para o conjunto de backup a ser restaurado. Por exemplo, especificar **1** indica o primeiro conjunto de backup na mídia de backup e **2** indica o segundo conjunto de backup.  
  
    -   (Opcional para dispositivos de fita) ** \@ Unload** – especifique um valor de **1** (padrão) se a fita deve ser descarregada da unidade após a conclusão da restauração e **0** se ela não deve ser descarregada.  
  
6.  (Opcional) Para uma assinatura pull, execute [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) e [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) no Assinante no banco de dados de assinatura. Para obter mais informações, consulte [Create a Pull Subscription](create-a-pull-subscription.md).  
  
7.  (Opcional) Iniciar o Distribution Agent. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) ou [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Copiar bancos de dados com backup e restauração](../databases/copy-databases-with-backup-and-restore.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
