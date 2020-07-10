---
title: sp_pdw_database_encryption_regenerate_system_keys (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
author: ronortloff
ms.author: rortloff
ms.reviewer: ''
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 06ce871e8f67a9cf4fa57b81eb84f47161e8fd28
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197327"
---
# <a name="sp_pdw_database_encryption_regenerate_system_keys-sql-data-warehouse"></a>sp_pdw_database_encryption_regenerate_system_keys (SQL Data Warehouse)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Use o **sp_pdw_database_encryption_regenerate_system_keys** para girar o certificado e a chave de criptografia do banco de dados para bancos internos que são criptografados quando o TDE está habilitado no dispositivo. Isso inclui o `tempdb`. Isso só terá sucesso se o TDE estiver habilitado.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 O procedimento não tem parâmetros.  
  
 Esse procedimento deve ser usado quando o tráfego no dispositivo estiver baixo.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de banco de dados fixa **sysadmin** ou a permissão **Control Server** .  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir regenera as chaves de criptografia do banco de dados.  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
