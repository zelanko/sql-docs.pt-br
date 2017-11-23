---
title: sp_pdw_database_encryption (SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e70d3a09e94a5e54f119934ec2c63ea90fa932f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_database_encryption** para habilitar a criptografia transparente de dados para um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] dispositivo. Quando **sp_pdw_database_encryption** definido como 1, use o **ALTER DATABASE** instrução para criptografar um banco de dados usando TDE.  
  
## <a name="syntax"></a>Sintaxe  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>Parâmetros  
 [  **@enabled=** ] *habilitado*  
 Determina se a criptografia transparente de dados está habilitada. *habilitado* é **int**, e pode ser um dos seguintes valores:  
  
-   0 = Desabilitado  
  
-   1 = Habilitado  
  
 Executar **sp_pdw_database_encryption** sem parâmetros retorna o estado atual da TDE no dispositivo como um conjunto de resultado escalar: 0 para desabilitado ou 1 para habilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando a TDE está habilitada usando **sp_pdw_database_encryption**, o banco de dados tempdb é descartado, recriado e criptografado. Por esse motivo, a TDE não pode ser habilitado em um dispositivo enquanto houver outras sessões ativas usando tempdb. Habilitando ou desabilitando a TDE em um dispositivo é uma ação que altera o estado do dispositivo, na maioria dos casos é esperada para ser executada uma vez no tempo de vida de dispositivo e deve ser executada quando não há nenhum tráfego no dispositivo.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **sysadmin** função de banco de dados fixa ou **CONTROL SERVER** permissão.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita TDE no dispositivo.  
  
```tsql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_pdw_database_encryption_regenerate_system_keys &#40; SQL Data Warehouse &#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40; SQL Data Warehouse &#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
