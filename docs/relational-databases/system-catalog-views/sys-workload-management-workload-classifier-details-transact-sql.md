---
title: sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/08/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: e4b884f779de2bf535b58d88659efffbd7901627
ms.sourcegitcommit: aa8bec762be29a29aed651d98ed4d868da85ba67
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57975359"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (Transact-SQL) (Preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Retorna detalhes de cada classificador.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID do classificador. Junções para [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md). Não permite valor nulo.|
|classifier_type|**sysname**|A entidade na qual a classificação está sendo feita. Não permite valor nulo.|[Classificação de carga de trabalho do SQL DATA Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)|
|classifier_value|**sysname**|O valor do classificador. Não permite valor nulo.||

## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.

## <a name="next-steps"></a>Próximas etapas
  
 Para obter uma lista de todas as exibições de catálogo para o SQL Data Warehouse e Parallel Data Warehouse, consulte [SQL Data Warehouse e exibições do catálogo Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para criar um classificador de carga de trabalho, consulte [CLASSIFICADOR de carga de trabalho criar](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obter mais informações sobre a classificação de carga de trabalho consulte [classificação de carga de trabalho do SQL DATA Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
