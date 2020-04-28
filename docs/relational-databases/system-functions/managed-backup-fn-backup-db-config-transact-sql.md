---
title: managed_backup. fn_backup_db_config (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_backup_db_config
- smart_admin.fn_backup_db_config_TSQL
- fn_backup_db_config
- fn_backup_db_config_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_db_config
- fn_backup_db_config
ms.assetid: 7c755d8a-64dd-44b2-be5e-735d30758900
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a23f8eb64ae99b999cdf6b16f1c888383a88c147
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68067779"
---
# <a name="managed_backupfn_backup_db_config-transact-sql"></a>managed_backup. fn_backup_db_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna 0, 1 ou mais linhas com parâmetros de configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Retorna 1 linha para o banco de dados especificado ou retorna as informações de todos os bancos de dados configurados com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] na instância.  
  
 Use este procedimento armazenado para examinar ou determinar os parâmetros de configuração atuais do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados ou todos os bancos de dados em uma instância do SQL Server.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
managed_backup.fn_backup_db_config ('database_name' | '' | NULL)  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 @db_name  
 O nome do banco de dados. O @db_name parâmetro é **sysname**. Se uma cadeia de caracteres vazia ou um valor NULO for passado para esse parâmetro, as informações sobre todos os bancos de dados na instância do SQL Server serão retornadas.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|db_name|SYSNAME|nome do banco de dados.|  
|db_guid|UNIQUEIDENTIFIER|Identificador que identifica exclusivamente o banco de dados.|  
|is_availability_database|BIT|Se o banco de dados estiver participando de um grupo de disponibilidade. Um valor 1 indica que é um banco de dados de disponibilidade e o valor 0 indica que não é.|  
|is_dropped|BIT|Um valor 1 indica que esse é um banco de dados ignorado.|  
|credential_name|SYSNAME|O nome da credencial de SQL usado para realizar a autenticação na conta de armazenamento. O valor NULL indica que nenhuma credencial do SQL foi definida.|  
|retention_days|INT|O período de retenção atual em dias. O valor NULL indica que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] nunca foi configurado para esse banco de dados.|  
|is_managed_backup_enabled|INT|Indica se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado no momento para esse banco de dados. Um valor 1 indica que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado no momento e um valor 0 indica que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está desabilitado para este banco de dados.|  
|storage_url|NVARCHAR (1024)|A URL da conta de armazenamento.|  
|Encryption_algorithm|NCHAR (20)|Retorna o algoritmo de criptografia atual a ser usado na criptografia do backup.|  
|Encryptor_type|NCHAR(15)|Retorna a configuração do criptografador: certificado ou chave assimétrica.|  
|Encryptor_name|NCHAR(max_length_of_cert/asymm_key_name)|O nome do certificado ou da chave assimétrica.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a associação na função de banco de dados **db_backupoperator** com as permissões **ALTER ANY Credential** . O usuário não deve ser negado às permissões **View any Definition** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] a configuração para ' TestDB '  
  
 Para cada snippet de código, selecione 'tsql' no campo do atributo de idioma.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config('TestDB')  
```  
  
 O exemplo a seguir retorna a configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para todos os bancos de dados na instância do SQL Server na qual é executada.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL)  
```  
  
  
