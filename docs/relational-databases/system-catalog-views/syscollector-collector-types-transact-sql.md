---
title: syscollector_collector_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 889c23db91765fb70d713d34c1356aea2e71d9a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syscollectorcollectortypes-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre um tipo de coletor de um item de coleta.  
  
|Nome da coluna|Tipo de dados|Description|  
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
|**is_system**|**bit**|Ativado (1) ou desativado (0) para indicar se o tipo de coletor foi enviado com o coletor de dados ou se ele foi adicionado depois pelo **dc_admin**. Pode ser um tipo personalizado, desenvolvido internamente ou por um terceiro. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT para **dc_operator**, **dc_proxy**.  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Atualizado **collection_type_uid** nome de coluna para **collector_type_uid**.|  
|Corrigida a descrição para o **parameter_schema** coluna para indicar que o valor é anulável.|  
|Adicionado o **parameter_formatter** coluna.|  
|Corrigido o tipo de dados para o **collection_package_path** coluna e atualizada a descrição para indicar que o valor é anulável.|  
|Corrigido o tipo de dados para o **upload_package_path** coluna e atualizada a descrição para indicar que o valor é anulável.|  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
