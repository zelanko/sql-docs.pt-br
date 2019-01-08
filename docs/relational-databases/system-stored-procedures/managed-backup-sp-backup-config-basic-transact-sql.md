---
title: managed_backup.sp_backup_config_basic (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f3345e2b27a14285f3b9a3bfffd1ec95549ef124
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201815"
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura a [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configurações básicas para um banco de dados específico ou para uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Esse procedimento pode ser chamado em seu próprio para criar uma configuração básica de backup gerenciada. No entanto, se você planeja adicionar recursos avançados ou uma agenda personalizada, primeiro configure essas configurações usando [sp_backup_config_advanced &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) e [managed_backup.sp_ backup_config_schedule &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) antes de habilitar o backup gerenciado com este procedimento.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @enable_backup  
 Habilite ou desabilite o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados especificado. O @enable_backup está **BIT**. Parâmetro obrigatório ao configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a primeira instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você estiver alterando um existente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuração, esse parâmetro é opcional. Nesse caso, os valores de configuração especificados não retêm seus valores existentes.  
  
 @database_name  
 O nome do banco de dados para habilitar o backup gerenciado em um banco de dados específico.  
  
 @container_url  
 Uma URL que indica o local do backup. Quando @credential_name for NULL, essa URL é uma URL de SAS (assinatura) de acesso compartilhado para um contêiner de blob no armazenamento do Azure e os backups de usam o novo backup à funcionalidade de blob de bloco. Para obter mais informações, examine [Noções básicas sobre SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Quando @credential_name for especificado, em seguida, essa é uma URL de conta de armazenamento e os backups de usam o backup preterido para funcionalidade de blob de página.  
  
> [!NOTE]  
>  Apenas uma URL SAS tem suporte para esse parâmetro no momento.  
  
 @retention_days  
 O período de retenção para os arquivos de backup em dias. O @storage_url é INT. Isso é um parâmetro obrigatório ao configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pela primeira vez na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao alterar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuração, esse parâmetro é opcional. Se não for especificado, os valores de configuração existentes serão retidos.  
  
 @credential_name  
 O nome da credencial de SQL usado para realizar a autenticação na conta de armazenamento do Windows Azure. @credentail_name está **SYSNAME**. Quando especificado, o backup é armazenado em um blob de página. Se esse parâmetro for NULL, o backup será armazenado como um blob de blocos. Backup para o blob de página foi preterido, portanto, é preferível usar a nova funcionalidade de backup de blob do bloco. Quando usado para alterar a configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], esse parâmetro é opcional. Se não for especificado, os valores de configuração existentes são mantidos.  
  
> [!WARNING]
>  O **@credential_name** parâmetro não é suportado no momento. Somente backup para blob de blocos é suportado, que requer esse parâmetro como NULL.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer associação na **db_backupoperator** função de banco de dados com **ALTER ANY CREDENTIAL** permissões, e **EXECUTE** permissões em **sp_delete backuphistory** procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
 Você pode criar o contêiner da conta de armazenamento e a URL SAS usando os comandos do PowerShell do Azure mais recente. O exemplo a seguir cria um novo contêiner, mycontainer, na conta de armazenamento mystorageaccount e, em seguida, obtém uma URL SAS para ela com permissões totais.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 O exemplo a seguir habilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a instância do SQL Server que é executado, define a política de retenção como 30 dias, define o destino para um contêiner denominado 'mycontainer' em uma conta de armazenamento denominada 'mystorageaccount'.  
  
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
  
  
