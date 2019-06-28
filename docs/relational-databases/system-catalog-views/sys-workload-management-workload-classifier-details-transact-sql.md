---
title: sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: d5494cb7e8fc49e9aa6e8335d0c65e6415375a1a
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413091"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql"></a>sys.workload_management_workload_classifier_details (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Retorna detalhes de cada classificador.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID do classificador. Junções para [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md). Não permite valor nulo.|
|classifier_type|**sysname**|A entidade na qual a classificação está sendo feita. Não permite valor nulo.|MEMBERNAME|
|classifier_value|**sysname**|O valor do classificador. Não permite valor nulo.||

## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.

## <a name="next-steps"></a>Próximas etapas
  
 Para obter uma lista de todas as exibições de catálogo para o SQL Data Warehouse e Parallel Data Warehouse, consulte [SQL Data Warehouse e exibições do catálogo Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para criar um classificador de carga de trabalho, consulte [CLASSIFICADOR de carga de trabalho criar](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obter mais informações sobre a classificação de carga de trabalho, consulte o SQL Data Warehouse [carga de trabalho de classificação](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) e [importância da carga de trabalho](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
