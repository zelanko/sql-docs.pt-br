---
description: managed_backup.sp_backup_config_basic (Transact-SQL)
title: managed_backup. sp_backup_config_basic (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 90ca851e5056b5c592b5cab67fc695f598b67ed1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481657"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Define as [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configurações básicas para um banco de dados específico ou para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Esse procedimento pode ser chamado por conta própria para criar uma configuração de backup gerenciado básico. No entanto, se você planeja adicionar recursos avançados ou uma agenda personalizada, primeiro defina essas configurações usando [managed_backup. sp_backup_config_advanced &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) e [managed_backup. sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) antes de habilitar o backup gerenciado com esse procedimento.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> Argumentos  
 @enable_backup  
 Habilite ou desabilite o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados especificado. O @enable_backup é o **bit**. Parâmetro obrigatório ao configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a primeira instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você estiver alterando uma [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuração existente, esse parâmetro será opcional. Nesse caso, quaisquer valores de configuração não especificados retêm seus valores existentes.  
  
 @database_name  
 O nome do banco de dados para habilitar o backup gerenciado em um banco de dados específico.  
  
 @container_url  
 Uma URL que indica o local do backup. Quando @credential_name é NULL, essa URL é uma URL de SAS (assinatura de acesso compartilhado) para um contêiner de blob no armazenamento do Azure e os backups usam o novo backup para bloquear a funcionalidade de BLOB. Para obter mais informações, consulte [noções básicas sobre SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Quando @credential_name é especificado, essa é uma URL de conta de armazenamento e os backups usam a funcionalidade de backup preterido para blob de páginas.  
  
> [!NOTE]  
>  Somente uma URL SAS tem suporte para esse parâmetro neste momento.  
  
 @retention_days  
 O período de retenção para os arquivos de backup em dias. O @storage_url é int. Esse é um parâmetro necessário ao configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] o pela primeira vez na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ao alterar a [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuração, esse parâmetro é opcional. Se não for especificado, os valores de configuração existentes serão retidos.  
  
 @credential_name  
 O nome da credencial SQL usada para autenticar para a conta de armazenamento do Azure. @credentail_name é **sysname**. Quando especificado, o backup é armazenado em um blob de páginas. Se esse parâmetro for nulo, o backup será armazenado como um blob de blocos. O backup em blob de páginas foi preterido, portanto, é preferível usar a nova funcionalidade de backup de blob de blocos. Quando usado para alterar a configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], esse parâmetro é opcional. Se não for especificado, os valores de configuração existentes serão mantidos.  
  
> [!WARNING]
>  Não há suporte para o parâmetro ** \@ credential_name** no momento. Há suporte apenas para backup em blob de blocos, o que exige que esse parâmetro seja nulo.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados **db_backupoperator** , com permissões **ALTER ANY Credential** e permissões **Execute** em **sp_delete_backuphistory** procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
 Você pode criar o contêiner da conta de armazenamento e a URL da SAS usando os comandos de Azure PowerShell mais recentes. O exemplo a seguir cria um novo contêiner, MyContainer, na conta de armazenamento mystorageaccount e, em seguida, obtém uma URL SAS para ele com permissões totais.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 O exemplo a seguir habilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] a instância do SQL Server em que é executado, define a política de retenção para 30 dias, define o destino para um contêiner chamado ' MyContainer ' em uma conta de armazenamento denominada ' mystorageaccount '.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [managed_backup. sp_backup_config_advanced &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
