---
title: Especificar destino de backup em disco ou fita
description: Este artigo mostra como especificar um disco ou uma fita como um destino de backup no SQL Server usando o SQL Server Management Studio ou o Transact-SQL.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- backup devices [SQL Server], disks
- disk backup devices [SQL Server]
- database backups [SQL Server], disks
- backing up databases [SQL Server], disks
- backups [SQL Server], creating
- tape backup devices, backing up
ms.assetid: e391f452-ed8c-4b40-b846-ac3881271b94
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d1a1d1975b5e71c8ed18200d07069f673e981732
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759067"
---
# <a name="specify-a-disk-or-tape-backup-destination-sql-server"></a>Especificar um disco ou fita como destino de backup (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve como especificar um disco ou uma fita como destino de backup no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  O suporte a dispositivos de backup em fita será removido em uma versão futura do SQL Server. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para especificar um disco ou uma fita como um destino de backup usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-specify-a-disk-or-tape-as-a-backup-destination"></a>Para especificar um disco ou uma fita como um destino de backup  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
  
4.  Na seção **Destino** da página **Geral** , clique em **Disco** ou **Fita**. Para selecionar os caminhos de até 64 unidades de disco ou fita que contêm um único conjunto de mídia, clique em **Adicionar**.  

   Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup, selecione-o e clique em **Conteúdo**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-specify-a-disk-or-tape-as-a-backup-destination"></a>Para especificar um disco ou uma fita como um destino de backup  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Na instrução [BACKUP](../../t-sql/statements/backup-transact-sql.md) , especifique o arquivo ou dispositivo e seu nome físico. Este exemplo executa o backup do banco de dados do `AdventureWorks2012` para o arquivo em disco `Z:\SQLServerBackups\AdventureWorks2012.Bak`.  
  
```  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)   
 [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
