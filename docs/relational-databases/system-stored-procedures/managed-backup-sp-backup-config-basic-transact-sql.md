---
title: managed_backup.sp_backup_config_basic (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f8f6a2bb437982bdc40c70b9e53c6c864dbc5b4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240056"
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configurações básicas para um banco de dados específico ou para uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Esse procedimento pode ser chamado em seu próprio para criar uma configuração básica de backup gerenciada. No entanto, se você planeja adicionar recursos avançados ou uma agenda personalizada, primeiro defina essas configurações usando [managed_backup. sp_backup_config_advanced &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) e [managed_backup.sp_ backup_config_schedule &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) antes de habilitar o backup gerenciado com este procedimento.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @enable_backup  
 Habilite ou desabilite o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados especificado. O @enable_backup é **BIT**. Parâmetro obrigatório ao configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a primeira instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você estiver alterando um existente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuração, esse parâmetro é opcional. Nesse caso, os valores de configuração especificados não mantém seus valores existentes.  
  
 @database_name  
 O nome do banco de dados para habilitar o backup gerenciado em um banco de dados específico.  
  
 @container_url  
 Uma URL que indica o local do backup. Quando @credential_name for NULL, essa URL é uma URL de SAS (assinatura) de acesso compartilhado para um contêiner de blob no armazenamento do Azure e os backups de usam o novo backup à funcionalidade de blob de bloco. Para obter mais informações, consulte [Noções básicas sobre SAS](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Quando @credential_name for especificado, essa é uma URL de conta de armazenamento e os backups de usam o backup preterido a funcionalidade de blob de página.  
  
> [!NOTE]  
>  Somente uma URL SAS tem suporte para esse parâmetro no momento.  
  
 @retention_days  
 O período de retenção para os arquivos de backup em dias. O @storage_url é INT. Este é um parâmetro obrigatório ao configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao alterar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuração, esse parâmetro é opcional. Se não for especificado, os valores de configuração existentes serão retidos.  
  
 @credential_name  
 O nome da credencial de SQL usado para realizar a autenticação na conta de armazenamento do Windows Azure. @credentail_name é **SYSNAME**. Quando especificado, o backup é armazenado em um blob de página. Se esse parâmetro for NULL, o backup será armazenado como um blob de bloco. Backup no blob de página foi preterido, é preferível usar a nova funcionalidade de backup de blob do bloco. Quando usado para alterar a configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], esse parâmetro é opcional. Se não for especificado, os valores de configuração existentes são mantidos.  
  
> [!WARNING]  
>  O **@credential_name** parâmetro não é suportado no momento. Somente backup para bloquear o blob tem suporte, que requer esse parâmetro como NULL.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a participação no **db_backupoperator** função, do banco de dados com **ALTER ANY CREDENTIAL** permissões, e **EXECUTE** permissões **sp_delete _ backuphistory** procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
 Você pode criar o contêiner de conta de armazenamento e a URL de SAS usando os comandos do PowerShell do Azure mais recentes. O exemplo a seguir cria um novo contêiner, mycontainer, na conta de armazenamento mystorageaccount e, em seguida, obtém uma URL SAS para ele com permissões totais.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 O exemplo a seguir habilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a instância do SQL Server que é executado, define a política de retenção de 30 dias, define o destino em um contêiner denominado 'mycontainer' conta de armazenamento denominada 'mystorageaccount'.  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 O exemplo a seguir desabilita o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a instância do SQL Server em que é executado.  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
