---
title: Procedimentos armazenados do SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 8dc5e634086c738399ce76090755466796cf3a69
ms.sourcegitcommit: 0a64d26f865a21f4bd967b2b72680fd8638770b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54395355"
---
# <a name="sql-data-warehouse-stored-procedures"></a>Procedimentos armazenados do SQL Data Warehouse
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Fornece procedimentos internos que você pode usar para executar operações relacionadas às funções de banco de dados. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inclui os seguintes procedimentos de sistema:  
  
##  <a name="AggregateFunctions"></a> [sp_datatype_info_90 &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  Alguns procedimentos armazenados são usados somente em uma instância do adicionais do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por meio do cliente são e APIs não se destina ao cliente usar. Esses procedimentos são listados em [procedimentos armazenados do sistema (Transact-SQL)](https://msdn.microsoft.com/library/ms187961.aspx). Estes procedimentos estão sujeitos a alterações e não há garantia de compatibilidade. Todos os procedimentos na lista não estão disponíveis em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Funções armazenadas do sistema &#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
