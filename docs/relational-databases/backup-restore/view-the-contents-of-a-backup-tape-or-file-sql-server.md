---
title: "Exibir o conteúdo de um arquivo ou fita de backup (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
- backup devices [SQL Server], tapes
- displaying backup content
- viewing backup content
- tape backup devices, viewing contents
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
ms.assetid: cd6674a2-ca55-4b5a-a971-878ba001821e
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e618ab96dac13911df7267009d17763c64813345
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="view-the-contents-of-a-backup-tape-or-file-sql-server"></a>Exibir o conteúdo de um arquivo ou fita de backup (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como exibir o conteúdo de uma fita ou arquivo de backup no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  O suporte a dispositivos de backup em fita será removido em uma versão futura do SQL Server. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir o conteúdo de um arquivo ou fita de backup, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações sobre segurança, veja [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
####  <a name="Permissions"></a> Permissões  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, a obtenção de informações sobre um conjunto ou dispositivo de backup exige a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>Para exibir o conteúdo de um arquivo ou fita de backup  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados do qual deseja fazer backup, aponte para **Tarefas**e clique em **Fazer Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
  
4.  Na seção **Destino** da página **Geral** , clique em **Disco** ou **Fita**. Na caixa de listagem **Backup para** , procure o arquivo em disco ou fita que deseja.  
  
     Se o arquivo em disco ou fita não for exibido na caixa de listagem, clique em **Adicionar**. Selecione um nome de arquivo ou unidade de fita. Para adicioná-lo à caixa de listagem **Fazer backup em** , clique em **OK**.  
  
5.  Na caixa de listagem **Fazer backup em** , selecione o caminho do disco ou da unidade de fita que você deseja exibir e clique em **Conteúdo**. Essa ação abre a caixa de diálogo **Conteúdos do dispositivo** .  
  
6.  O painel direito exibe informações sobre o conjunto de mídias definido e conjuntos de backup no arquivo ou fita selecionado.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>Para exibir o conteúdo de um arquivo ou fita de backup  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Use instrução [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) . Este exemplo retorna informações sobre o arquivo chamado `AdventureWorks2012-FullBackup.bak`:  
  
```sql  
USE AdventureWorks2012;  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks2012-FullBackup.bak' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
