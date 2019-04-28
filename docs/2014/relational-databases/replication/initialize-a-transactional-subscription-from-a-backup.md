---
title: Inicializar uma assinatura transacional de um Backup (programação Transact-SQL de replicação) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2101277aecd3ca9c844fb447f5ab772847d77020
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721111"
---
# <a name="initialize-a-transactional-subscription-from-a-backup-replication-transact-sql-programming"></a>Inicializar uma assinatura transacional de um backup (Programação Transact-SQL de replicação)
  Embora uma assinatura a uma publicação transacional seja geralmente inicializada com um instantâneo, é possível inicializar uma assinatura de backup usando procedimentos de replicação armazenados. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>Para inicializar um assinante transacional a partir de backup  
  
1.  Para uma publicação existente, certifique-se de que a publicação dê suporte à capacidade de inicializar do backup, executando [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) no Publicador no banco de dados de publicação. Observe o valor de **allow_initialize_from_backup** no conjunto de resultados.  
  
    -   Se o valor for **1**, a publicação oferece suporte a essa funcionalidade.  
  
    -   Se o valor for **0**, execute [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **allow_initialize_from_backup** para **@property** e um valor de `true` para **@value**.  
  
2.  Para uma nova publicação, execute [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de `true` para **allow_initialize_from_backup**. Para obter mais informações, consulte [Criar uma assinatura](publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Para evitar perder dados do assinante, ao usar **sp_addpublication** com `@allow_initialize_from_backup = N'true'`, sempre use `@immediate_sync = N'true'`.  
  
3.  Crie um backup do banco de dados de publicação usando a instrução [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
4.  Restaure o backup no Assinante usando a instrução [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
5.  No Publicador no banco de dados de publicação, execute o procedimento armazenado [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique os seguintes parâmetros:  
  
    -   **@sync_type** - valor para **inicializar com backup**.  
  
    -   **@backupdevicetype** - o tipo de dispositivo de backup: **lógico** (padrão), **disco**ou **fita**.  
  
    -   **@backupdevicename** - o dispositivo de backup lógico ou físico a usar para a restauração.  
  
         Para um dispositivo lógico, especifique o nome do dispositivo de backup especificado quando **sp_addumpdevice** foi usado para criar o dispositivo.  
  
         Para um dispositivo físico, especifique um caminho completo e nome de arquivo, como `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\BACKUP\Mybackup.dat'` ou `TAPE = '\\.\TAPE0'`.  
  
    -   (Opcional) **@password** - uma senha fornecida na criação do conjunto de backup.  
  
    -   (Opcional) **@mediapassword** - uma senha fornecida na formatação do conjunto de mídias.  
  
    -   (Opcional) **@fileidhint** - identificador para o conjunto de backup a ser restaurado. Por exemplo, especificar **1** indica o primeiro conjunto de backup na mídia de backup e **2** indica o segundo conjunto de backup.  
  
    -   (Opcional para dispositivos de fita) **@unload** - especifica um valor de **1** (padrão) se a fita deve ser descarregada da unidade depois de concluir a restauração e **0** se não deve ser descarregada.  
  
6.  (Opcional) Para uma assinatura pull, execute [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) e [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) no Assinante no banco de dados de assinatura. Para obter mais informações, consulte [Create a Pull Subscription](create-a-pull-subscription.md).  
  
7.  (Opcional) Iniciar o Distribution Agent. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) ou [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Consulte também  
 [Copiar bancos de dados com backup e restauração](../databases/copy-databases-with-backup-and-restore.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
