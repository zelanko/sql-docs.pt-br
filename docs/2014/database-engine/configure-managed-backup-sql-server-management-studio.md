---
title: Configurar o Backup gerenciado (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0403d34b48b74d0517aaf3cb31ea520dbc436f89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165596"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>Configurar o Backup Gerenciado (SQL Server Management Studio)
  O **Backup gerenciado** caixa de diálogo permite que você configure [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] padrões para a instância. Este tópico descreve como usar essa caixa de diálogo para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurações padrão para a instância e opções que você deve considerar ao fazer isso. Quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está configurado para a instância, as configurações são aplicadas a qualquer novo banco de dados criado depois disso.  
  
 Se você quiser configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados específico, consulte [habilitar e configurar SQL Server Managed Backup to Windows Azure para um banco de dados](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
 
> [!NOTE] 
> Não há suporte para backup gerenciado do SQL Server com servidores proxy. 
  
## <a name="task-list"></a>Lista de Tarefas  
  
## <a name="includesssmartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] Funções usando Interface Backup gerenciado no SQL Server Management Studio  
 Nesta versão, você só pode configurar as configurações padrão de nível de instância usando a interface **Backup de Gerenciamento** . Não é possível configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados, pausar ou retomar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] operações ou configurar notificações por email. Para obter informações sobre como executar operações sem suporte no momento por meio de **Backup gerenciado** interface, consulte [SQL Server Managed Backup to Windows Azure - Retention and Storage Settings](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
## <a name="permissions"></a>Permissões  
 **P Nó de Backup Gerenciado da exibição é o SQL Server Management Studio:** Para exibir o nó  **Backup gerenciado** no **Pesquisador de Objetos**, você deve ser um administrador do sistema ou ter as seguintes permissões concedidas especificamente à sua conta de usuário:  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE` em `smart_admin.fn_is_master_switch_on`.  
  
-   `SELECT` em `smart_admin.fn_backup_instance_config`.  
  
 **Para configurar o Backup gerenciado:** para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no SQL Server Management Studio, você deve ser um administrador do sistema ou ter as seguintes permissões:  
  
 Associação na `db_backupoperator` função de banco de dados com `ALTER ANY CREDENTIAL` permissões, e `EXECUTE` permissões em `sp_delete_backuphistory` procedimento armazenado.  
  
 `SELECT` permissões de `smart_admin.fn_get_current_xevent_settings` função.  
  
 `EXECUTE` permissões no `smart_admin.sp_get_backup_diagnostics` procedimento armazenado. Além disso, requer permissões `VIEW SERVER STATE`, pois chama internamente outros objetos do sistema que exigem essa permissão.  
  
 `EXECUTE` permissões no `smart_admin.sp_set_instance_backup`, e `smart_admin.sp_backup_master_switch`.  
  
## <a name="configure-includesssmartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>Configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando o SQL Server Management Studio  
 Do **Pesquisador de Objetos**, expanda o nó **Gerenciamento** e clique com o botão direito do mouse em **Backup Gerenciado**. Selecione **Configurar**. Essa ação abre a caixa de diálogo **Backup Gerenciado** .  
  
 Marque a opção **Habilitar Backup Gerenciado** e especifique os valores de configuração:  
  
 O período de **Retenção de arquivos** é especificado em dias e deve estar entre 1 e 30.  
  
 A **Credencial SQL** que você seleciona deve corresponder à conta de armazenamento. Se atualmente você não tiver uma credencial do SQL que armazene as informações de autenticação, você pode criar uma clicando em **Criar**. Também pode criar credenciais usando a instrução Transact-SQL CREATE CREDENTIAL, além de fornecer o nome da conta de armazenamento para Identidade e a chave de acesso para os parâmetros SECRET. Para obter mais informações, consulte [criar uma credencial](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential).  
  
 Especifique a **URL de armazenamento** para a conta de armazenamento do Microsoft Azure, a credencial do SQL que armazena as informações de autenticação da conta de armazenamento e o período de retenção para os arquivos de backup.  
  
 É o formato de URL de armazenamento: https://\<StorageAccount >.blob.core.windows.net/  
  
 Para definir as configurações de criptografia no nível da instância, marque a opção **Criptografar Backup** e especifique o algoritmo e um certificado ou chave assimétrica a serem usados na criptografia.  Isso é definido no nível da instância e é usado para todos os novos bancos de dados criados depois de essa configuração ser aplicada.  
  
> [!WARNING]  
>  Essa caixa de diálogo não pode ser usada para especificar as opções de criptografia sem configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Essas opções de criptografia só se aplicam a [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] operações. Para usar criptografia para outros procedimentos de backup, consulte [criptografia de Backup](../relational-databases/backup-restore/backup-encryption.md).  
  
### <a name="considerations"></a>Considerações  
 Se você configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível de instância, as configurações são aplicadas a qualquer novo banco de dados criado depois disso.  No entanto, bancos de dados existentes não herdarão essas configurações automaticamente. Para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] em bancos de dados existentes, você deve configurar cada banco de dados especificamente. Para obter mais informações, consulte [habilitar e configurar SQL Server Managed Backup to Windows Azure para um banco de dados](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
  
 Se [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] foi pausado usando o `smart_admin.sp_backup_master_switch`, você verá uma mensagem de aviso "o Backup gerenciado está desabilitado e as configurações atuais não entrarão em vigor..." quando tentar concluir a configuração. Use o `smart_admin.sp_backup_master_switch` armazenado e defina o @new_state= 1. Isso retomará [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] serviços e as definições de configuração entrarão em vigor. Para obter mais informações sobre o procedimento armazenado, consulte [smart_admin.sp_ backup_master_switch &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [Backup Gerenciado do SQL Server para o Microsoft Azure: Interoperabilidade e coexistência](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
