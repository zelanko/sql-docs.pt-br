---
title: "Inicializar uma assinatura transacional de um backup (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "inicialização manual de assinaturas [replicação do SQL Server]"
  - "assinaturas [replicação do SQL Server], inicializando"
  - "inicializando assinaturas [replicação do SQL Server], sem instantâneos"
  - "replicação transacional, backup e restauração"
  - "backups [replicação do SQL Server], replicação transacional"
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Inicializar uma assinatura transacional de um backup (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Embora uma assinatura a uma publicação transacional seja geralmente inicializada com um instantâneo, é possível inicializar uma assinatura de backup usando procedimentos de replicação armazenados. Para obter mais informações, consulte [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### Para inicializar um assinante transacional a partir de backup  
  
1.  Para uma publicação existente, certifique-se de que a publicação oferece suporte a capacidade de inicializar a partir do backup executando [sp_helppublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) o publicador do banco de dados de publicação. Observe o valor de **allow_initialize_from_backup** no conjunto de resultados.  
  
    -   Se o valor for **1**, a publicação oferece suporte a essa funcionalidade.  
  
    -   Se o valor for **0**, execute [sp_changepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) o publicador do banco de dados de publicação. Especifique um valor de **allow_initialize_from_backup** para **@property** e um valor de **true** para **@value**.  
  
2.  Para uma nova publicação, execute [sp_addpublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) o publicador do banco de dados de publicação. Especifique um valor de **true** para **allow_initialize_from_backup**. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Para evitar perder dados do assinante, ao usar **sp_addpublication** com `@allow_initialize_from_backup = N'true'`, sempre use `@immediate_sync = N'true'`.  
  
3.  Criar um backup do banco de dados de publicação usando o [BACKUP & #40. O Transact-SQL e 41;](../../t-sql/statements/backup-transact-sql.md) instrução.  
  
4.  Restaure o backup no assinante usando o [40; & RESTAURAR O Transact-SQL e 41;](../Topic/RESTORE%20\(Transact-SQL\).md) instrução.  
  
5.  O publicador do banco de dados de publicação, execute o procedimento armazenado [sp_addsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique os seguintes parâmetros:  
  
    -   **@sync_type** -um valor de **inicializar com backup**.  
  
    -   **@backupdevicetype** -o tipo de dispositivo de backup: **lógica** (padrão), **disco**, ou **fita**.  
  
    -   **@backupdevicename** -o dispositivo de backup lógico ou físico a ser usado para a restauração.  
  
         Para um dispositivo lógico, especifique o nome do dispositivo de backup especificado quando **sp_addumpdevice** foi usado para criar o dispositivo.  
  
         Para um dispositivo físico, especifique um caminho completo e nome de arquivo, como `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` ou `TAPE = '\\.\TAPE0'`.  
  
    -   (Opcional) **@password** -uma senha que foi fornecida quando o conjunto de backup foi criado.  
  
    -   (Opcional) **@mediapassword** -uma senha que foi fornecida quando o conjunto de mídias foi formatado.  
  
    -   (Opcional) **@fileidhint** -identificador para o conjunto de backup a ser restaurado. Por exemplo, a especificação **1** indica o primeiro backup definido na mídia de backup e **2** indica o segundo conjunto de backup.  
  
    -   (Opcional para dispositivos de fita) **@unload** -Especifique um valor de **1** (padrão) se a fita deve ser descarregada da unidade após a restauração for concluída e **0** se ele não deve ser descarregado.  
  
6.  (Opcional) Para uma assinatura pull, execute [sp_addpullsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) e [sp_addpullsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) no assinante no banco de dados de assinatura. Para obter mais informações, confira [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
7.  (Opcional) Iniciar o Distribution Agent. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) ou [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## Consulte também  
 [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  