---
title: syscollector_collector_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collector_types
- syscollector_collector_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collector_types view
ms.assetid: d5cd30bb-89fd-4814-a7e8-9074f043f90f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d1ff2329d0070d554f87e405a6030b744e98d23a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896750"
---
# <a name="syscollector_collector_types-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fornece informações sobre um tipo de coletor de um item de coleta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifer**|O GUID de um tipo de coleta. Não permite valor nulo.|  
|**name**|**sysname**|O nome do tipo de coleta. Não permite valor nulo.|  
|**parameter_schema**|**xml**|O esquema XML que descreve a aparência da configuração do tipo de coletor especificado. Este esquema XML é usado para validar a configuração XML atual associada a uma instância de item de coleta específica. Permite valor nulo.|  
|**parameter_formatter**|**xml**|Determina o modelo a ser usado para transformar o XML para uso na página de propriedades do conjunto de coleta. Permite valor nulo.|  
|**collection_package_id**|**uniqueidentifer**|O GUID de um pacote de coleta. Não permite valor nulo.|  
|**collection_package_path**|**nvarchar(4000)**|Fornece o caminho para o pacote de coleta. Permite valor nulo.|  
|**collection_package_name**|**sysname**|O nome do pacote de coleta. Não permite valor nulo.|  
|**upload_package_id**|**uniqueidentifer**|O GUID do pacote de carregamento. Não permite valor nulo.|  
|**upload_package_path**|**nvarchar(4000)**|Fornece o caminho para o pacote de carregamento. Permite valor nulo.|  
|**upload_package_name**|**sysname**|O nome do pacote de carregamento. Não permite valor nulo.|  
|**is_system**|**bit**|Ativado (1) ou desativado (0) para indicar se o tipo de coletor foi enviado com o coletor de dados ou se foi adicionado posteriormente pelo **dc_admin**. Pode ser um tipo personalizado, desenvolvido internamente ou por um terceiro. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT for **dc_operator**, **dc_proxy**.  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Atualizado **collection_type_uid** nome da coluna para **collector_type_uid**.|  
|Correção da descrição da coluna **parameter_schema** para indicar que o valor é anulável.|  
|Adicionada a coluna **parameter_formatter** .|  
|Corrigido o tipo de dados para a coluna **collection_package_path** e a descrição foi atualizada para indicar que o valor é anulável.|  
|Corrigido o tipo de dados para a coluna **upload_package_path** e a descrição foi atualizada para indicar que o valor é anulável.|  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do coletor de dados &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)  
  
  
