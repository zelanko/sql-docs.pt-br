---
description: sp_pdw_database_encryption (Azure Synapse Analytics)
title: sp_pdw_database_encryption (Azure Synapse Analytics) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f8d77853846a18bd310d8afa58101cf66a24475b
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92258087"
---
# <a name="sp_pdw_database_encryption-azure-synapse-analytics"></a>sp_pdw_database_encryption (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Use **sp_pdw_database_encryption** para habilitar a Transparent Data Encryption em para um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] dispositivo. Quando **sp_pdw_database_encryption** definido como 1, use a instrução **ALTER DATABASE** para criptografar um banco de dados usando TDE.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

#### <a name="parameters"></a>Parâmetros  
`[ @enabled = ] enabled` Determina se a criptografia de dados transparente está habilitada. *habilitado* é **int**e pode ser um dos seguintes valores:  
  
-   0 = Desabilitado  
  
-   1 = Habilitado  
  
 A execução de **sp_pdw_database_encryption** sem parâmetros retorna o estado atual de TDE no dispositivo como um conjunto de resultados escalar: 0 para desabilitado ou 1 para habilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando o TDE é habilitado usando **sp_pdw_database_encryption**, o banco de dados tempdb é Descartado, recriado e criptografado. Por esse motivo, o TDE não pode ser habilitado em um dispositivo enquanto houver outras sessões ativas usando o tempdb. Habilitar ou desabilitar o TDE em um dispositivo é uma ação que altera o estado do dispositivo, na maioria dos casos, espera-se que seja executado uma vez no tempo de vida do dispositivo e deve ser executado quando não houver tráfego no dispositivo.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de banco de dados fixa **sysadmin** ou a permissão **Control Server** .  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita o TDE no dispositivo.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>Confira também  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
