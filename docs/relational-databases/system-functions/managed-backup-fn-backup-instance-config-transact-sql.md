---
title: managed_backup.fn_backup_instance_config (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4dae80911e6508a1a398cf208300bf4145faeecc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970498"
---
# <a name="managedbackupfnbackupinstanceconfig-transact-sql"></a>managed_backup.fn_backup_instance_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna 1 linha com os parâmetros de configuração padrão de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] da instância do SQL Server.  
  
 Use este procedimento armazenado para examinar ou determinar os parâmetros de configuração padrão de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a instância do SQL Server.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="Arguments"></a> Argumentos  
 Nenhum  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|Exibe 1 quando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitado e 0 quando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está desabilitado.|  
|credential_name|SYSNAME|A Credencial SQL padrão é usada para realizar a autenticação no armazenamento.|  
|retention_days|INT|Período de retenção padrão definido no nível da instância.|  
|storage_url|NVARCHAR(1024)|A URL padrão da conta de armazenamento definida no nível de instância.|  
|encryption_algorithm|SYSNAME|Nome do algoritmo de criptografia. Será definido como NULL se a criptografia não for especificada.|  
|encryptor_type|NVARCHAR(32)|O tipo de criptografador usado: certificado ou chave assimétrica. Será definido como NULL se não houver criptografador especificado.|  
|encryptor_name|SYSNAME|O nome do certificado ou da chave assimétrica. Será definido como NULL se não houver nome especificado|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer associação na **db_backupoperator** função de banco de dados com **ALTER ANY CREDENTIAL** permissões. O usuário não deve ser negado **VIEW ANY DEFINITION** permissões.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os parâmetros de configuração padrão de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] da instância na qual ele é executado.  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
