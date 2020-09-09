---
description: syscollector_config_store (Transact-SQL)
title: syscollector_config_store (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_config_store_TSQL
- syscollector_config_store
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_config_store view
ms.assetid: f15f6b05-6808-4b76-b6a8-48dec844cf63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4ceeb3ad0d977282c88314a7305099f7c0db0496
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537667"
---
# <a name="syscollector_config_store-transact-sql"></a>syscollector_config_store (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna as propriedades que se aplicam a todo o coletor de dados em vez de apenas uma instância do conjunto de coleta. Cada linha nesta exibição descreve uma propriedade específica do coletor de dados, como o nome do data warehouse de gerenciamento e o nome da instância em que o data warehouse de gerenciamento está situado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|parameter_name|**nvarchar(128)**|O nome da propriedade. Não permite valor nulo.|  
|parameter_value|**sql_variant**|O valor real da propriedade. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão SELECT na exibição ou associação nas funções de banco de dados fixas dc_operator, dc_proxy ou dc_admin.  
  
## <a name="remarks"></a>Comentários  
 A lista de propriedades disponíveis é fixa e seus valores só podem ser alterados por meio do procedimento armazenado apropriado. A tabela a seguir descreve as propriedades que são expostas por esta exibição.  
  
|Nome da propriedade|Descrição|  
|-------------------|-----------------|  
|CacheDirectory|O nome do diretório no sistema de arquivo onde os pacotes de tipo de coletor armazenam informações temporárias.<br /><br /> NULL = o diretório temporário padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é usado.|  
|CacheWindow|Indica a política de retenção de dados do diretório de cache para cargas de dados com falha.<br /><br /> -1 = Retém os dados de todas as falhas de carga.<br /><br /> 0 = Não retém nenhum dado das falhas de carga.<br /><br /> *n* = reter dados de *n* falhas de carregamento anteriores, em que *n* >= 1.<br /><br /> Use o procedimento armazenado sp_syscollector_set_cache_window para alterar esse valor.|  
|CollectorEnabled|Indica o estado do coletor de dados.<br /><br /> 0 = desabilitado<br /><br /> 1 = habilitado<br /><br /> Use o procedimento armazenado sp_syscollector_enable_collector ou sp_syscollector_disable_collector para alterar esse valor.|  
|MDWDatabase|O nome do data warehouse de gerenciamento. Use o procedimento armazenado sp_syscollector_set_warehouse_database_name para alterar esse valor.|  
|MDWInstance|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o data warehouse de gerenciamento. Use o procedimento armazenado sp_syscollector_set_warehouse_instance_name para alterar este valor.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir consulta a exibição syscollector_config_store.  
  
```sql  
SELECT parameter_name, parameter_value  
FROM msdb.dbo.syscollector_config_store;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_syscollector_set_warehouse_database_name ](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_syscollector_set_warehouse_instance_name ](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
