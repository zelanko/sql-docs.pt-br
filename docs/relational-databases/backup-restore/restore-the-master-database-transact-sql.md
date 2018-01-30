---
title: Restaurar o banco de dados mestre (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bdcb8f41a3eb6abd20f905f573f84fb1b426f014
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="restore-the-master-database-transact-sql"></a>Restaurar o banco de dados mestre (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico explica como restaurar o banco de dados **master** com base em um backup de banco de dados completo.  
  
### <a name="to-restore-the-master-database"></a>Para restaurar o banco de dados mestre  
  
1.  Inicie uma instância de servidor no modo de usuário único.  
  
     Para obter informações sobre como especificar o parâmetro de inicialização de usuário único (**-m**), veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
2.  Para restaurar um backup de banco de dados completo do **master**, use a seguinte instrução [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `RESTORE DATABASE master FROM`  *<backup_device>*  `WITH REPLACE`  
  
     A opção REPLACE instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a restaurar o banco de dados especificado mesmo quando um banco de dados do mesmo nome já existir. O banco de dados existente, se houver, será excluído. Em modo de usuário único, é recomendável inserir a instrução RESTORE DATABASE no [utilitário sqlcmd](../../tools/sqlcmd-utility.md). Para obter mais informações, consulte [Usar o Utilitário sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
    > [!IMPORTANT]  
    >  Depois que o **master** é restaurado, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é encerrada e o processo **sqlcmd** é concluído. Antes de reiniciar a instância do servidor, remova o parâmetro de inicialização de usuário único. Para obter mais informações, veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
3.  Reinicie a instância do servidor e continue outras etapas de recuperação, como restaurar outros bancos de dados, anexar bancos de dados e corrigir incompatibilidades de usuário.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir restaura o banco de dados `master` na instância do servidor padrão. O exemplo assume que a instância do servidor já está sendo executada no modo de usuário único. O exemplo inicia o `sqlcmd` e executa uma instrução `RESTORE DATABASE` que restaura um backup de banco de dados completo de `master` de um dispositivo de disco: `Z:\SQLServerBackups\master.bak`.  
  
> [!NOTE]  
>  Para uma instância nomeada, o comando **sqlcmd** deve especificar a opção **-S***\<ComputerName>*\\*\<InstanceName>*.  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Recriar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)   
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
