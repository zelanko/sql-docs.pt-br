---
title: Configurar o backup gerenciado (SQL Server Management Studio) | Microsoft Docs
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
ms.openlocfilehash: 021db5a2283eb6ec68ea80302e938f08e7ba1a5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70154337"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>Configurar o Backup Gerenciado (SQL Server Management Studio)
  A caixa de diálogo **Backup gerenciado** permite que você configure padrões do [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para a instância. Este tópico descreve como usar essa caixa de diálogo para configurar configurações padrão [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para a instância e opções que você deve considerar ao fazer isso. Quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está configurado para a instância, as configurações são aplicadas a qualquer novo banco de dados criado depois disso.  
  
 Se você quiser configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o para um banco de dados específico, consulte [habilitar e configurar SQL Server Backup gerenciado para o Azure para um banco de dados](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
 
> [!NOTE] 
> Não há suporte para backup gerenciado do SQL Server com servidores proxy. 
  
## <a name="task-list"></a>Lista de Tarefas  
  
## <a name="ss_smartbackup-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] Funções usando Interface Backup Gerenciado no SQL Server Management Studio  
 Nesta versão, você só pode configurar as configurações padrão de nível de instância usando a interface **Backup de Gerenciamento** . Não é possível configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para um banco de dados, pausar ou retomar operações [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] , nem configurar notificações por email. Para obter informações sobre como executar operações que não têm suporte no momento por meio da interface de **backup gerenciado** , consulte [SQL Server Backup gerenciado para o Azure – retenção e configurações de armazenamento](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
## <a name="permissions"></a>Permissões  
 **P Nó de Backup Gerenciado da exibição é o SQL Server Management Studio:** Para exibir o nó  **Backup gerenciado** no **Pesquisador de Objetos**, você deve ser um administrador do sistema ou ter as seguintes permissões concedidas especificamente à sua conta de usuário:  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE`em `smart_admin.fn_is_master_switch_on`.  
  
-   `SELECT`em `smart_admin.fn_backup_instance_config`.  
  
 **Para configurar o Backup gerenciado:** para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no SQL Server Management Studio, você deve ser um administrador do sistema ou ter as seguintes permissões:  
  
 Associação na função de banco de dados `db_backupoperator`, com permissões `ALTER ANY CREDENTIAL` e permissões `EXECUTE` no procedimento armazenado `sp_delete_backuphistory`.  
  
 `SELECT`permissões na `smart_admin.fn_get_current_xevent_settings` função.  
  
 `EXECUTE`permissões no procedimento `smart_admin.sp_get_backup_diagnostics` armazenado. Além disso, requer permissões `VIEW SERVER STATE`, pois chama internamente outros objetos do sistema que exigem essa permissão.  
  
 Permissões `EXECUTE` em `smart_admin.sp_set_instance_backup` e `smart_admin.sp_backup_master_switch`.  
  
## <a name="configure-ss_smartbackup-using-sql-server-management-studio"></a>Configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usando o SQL Server Management Studio  
 Do **Pesquisador de Objetos**, expanda o nó **Gerenciamento** e clique com o botão direito do mouse em **Backup Gerenciado**. Selecione **Configurar**. Essa ação abre a caixa de diálogo **Backup Gerenciado** .  
  
 Marque a opção **Habilitar Backup Gerenciado** e especifique os valores de configuração:  
  
 O período de **Retenção de arquivos** é especificado em dias e deve estar entre 1 e 30.  
  
 A **Credencial SQL** que você seleciona deve corresponder à conta de armazenamento. Se atualmente você não tiver uma credencial do SQL que armazene as informações de autenticação, você pode criar uma clicando em **Criar**. Também pode criar credenciais usando a instrução Transact-SQL CREATE CREDENTIAL, além de fornecer o nome da conta de armazenamento para Identidade e a chave de acesso para os parâmetros SECRET. Para obter mais informações, consulte [Create a Credential](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential).  
  
 Especifique a **URL de armazenamento** para a conta de armazenamento do Azure, a credencial SQL que armazena as informações de autenticação para a conta de armazenamento e o período de retenção para os arquivos de backup.  
  
 O formato da URL de armazenamento é\<: https://StorageAccount>. blob.Core.Windows.net/  
  
 Para definir as configurações de criptografia no nível da instância, marque a opção **Criptografar Backup** e especifique o algoritmo e um certificado ou chave assimétrica a serem usados na criptografia.  Isso é definido no nível da instância e é usado para todos os novos bancos de dados criados depois de essa configuração ser aplicada.  
  
> [!WARNING]  
>  Essa caixa de diálogo não pode ser usada para especificar as opções de criptografia sem configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Essas opções de criptografia só se aplicam a operações [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] . Para usar criptografia para outros procedimentos de backup, consulte [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).  
  
### <a name="considerations"></a>Considerações  
 Se você configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no nível de instância, as configurações são aplicadas a qualquer novo banco de dados criado depois disso.  No entanto, bancos de dados existentes não herdarão essas configurações automaticamente. Para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] em bancos de dados existentes, você deve configurar cada banco de dados especificamente. Para obter mais informações, consulte [habilitar e configurar SQL Server Backup gerenciado para o Azure para um banco de dados](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
  
 Se [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o tiver sido pausado usando `smart_admin.sp_backup_master_switch`o, você verá uma mensagem de aviso "o backup gerenciado está desabilitado e as configurações atuais não entrarão em vigor..." Quando você tenta concluir a configuração. Use o `smart_admin.sp_backup_master_switch` armazenado e defina o @new_state= 1. Isso retomará os serviços [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] e as definições de configuração entrarão em vigor. Para obter mais informações sobre o procedimento armazenado, consulte [smart_admin. sp_ backup_master_switch &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Backup gerenciado do SQL Server para o Azure: interoperabilidade e coexistência](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
