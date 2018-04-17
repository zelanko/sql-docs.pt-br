---
title: managed_backup.fn_backup_db_config (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a3cf62f8d658136c7bab304a6f4c73d62c77ba4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="managedbackupfnbackupdbconfig-transact-sql"></a>managed_backup.fn_backup_db_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna 0, 1 ou mais linhas com parâmetros de configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Retorna 1 linha para o banco de dados especificado ou retorna as informações de todos os bancos de dados configurados com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] na instância.  
  
 Use este procedimento armazenado para examinar ou determinar os parâmetros de configuração atuais do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para o banco de dados ou todos os bancos de dados em uma instância do SQL Server.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
managed_backup.fn_backup_db_config (‘database_name’ | ‘’ | NULL)  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @db_name  
 O nome do banco de dados. O @db_name parâmetro é **SYSNAME**. Se uma cadeia de caracteres vazia ou um valor NULO for passado para esse parâmetro, as informações sobre todos os bancos de dados na instância do SQL Server serão retornadas.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|db_name|SYSNAME|Nome do banco de dados.|  
|db_guid|UNIQUEIDENTIFIER|Identificador que identifica exclusivamente o banco de dados.|  
|is_availability_database|BIT|Se o banco de dados estiver participando de um grupo de disponibilidade. Um valor 1 indica que é um banco de dados de disponibilidade e o valor 0 indica que não é.|  
|is_dropped|BIT|Um valor 1 indica que esse é um banco de dados ignorado.|  
|credential_name|SYSNAME|O nome da credencial de SQL usado para realizar a autenticação na conta de armazenamento. O valor NULL indica que nenhuma credencial do SQL foi definida.|  
|retention_days|INT|O período de retenção atual em dias. O valor NULL indica que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] nunca foi configurado para esse banco de dados.|  
|is_smart_backup_enabled|INT|Indica se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado no momento para esse banco de dados. Um valor 1 indica que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado no momento e um valor 0 indica que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está desabilitado para este banco de dados.|  
|storage_url|NVARCHAR(1024)|A URL da conta de armazenamento.|  
|Encryption_algorithm|NCHAR(20)|Retorna o algoritmo de criptografia atual a ser usado na criptografia do backup.|  
|Encryptor_type|NCHAR(15)|Retorna a configuração do criptografador: certificado ou chave assimétrica.|  
|Encryptor_name|NCHAR(max_length_of_cert/asymm_key_name)|O nome do certificado ou da chave assimétrica.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a participação no **db_backupoperator** função de banco de dados com **ALTER ANY CREDENTIAL** permissões. O usuário não deve ser negado **VIEW ANY DEFINITION** permissões.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para ‘TestDB’.  
  
 Para cada trecho de código, selecione 'tsql' no campo do atributo de idioma.  
  
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
  
  
