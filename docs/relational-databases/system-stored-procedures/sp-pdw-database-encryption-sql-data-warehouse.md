---
title: sp_pdw_database_encryption (SQL Data Warehouse) | Microsoft Docs
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
ms.openlocfilehash: 47d7aca62ddbf2637b54d77171a08817b842555c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008916"
---
# <a name="sp_pdw_database_encryption-sql-data-warehouse"></a>sp_pdw_database_encryption (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_database_encryption** para habilitar a Transparent Data Encryption [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] em para um dispositivo. Quando **sp_pdw_database_encryption** definido como 1, use a instrução **ALTER DATABASE** para criptografar um banco de dados usando TDE.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>parâmetros  
`[ @enabled = ] enabled`Determina se a criptografia de dados transparente está habilitada. *habilitado* é **int**e pode ser um dos seguintes valores:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
