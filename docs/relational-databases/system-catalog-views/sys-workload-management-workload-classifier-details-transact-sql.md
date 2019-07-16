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
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: f9314b9297af7e8156ed86b2bfa2dadd18896bb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061292"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql"></a>sys.workload_management_workload_classifier_details (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Retorna detalhes de cada classificador.  
  
|Nome da coluna|Tipo de dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID do classificador. Junções para [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md). Não permite valor nulo.|
|classifier_type|**sysname**|A entidade na qual a classificação está sendo feita. Não permite valor nulo.|NOME DO MEMBRO|
|classifier_value|**sysname**|O valor do classificador. Não permite valor nulo.||

## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.

## <a name="next-steps"></a>Próximas etapas
  
 Para obter uma lista de todas as exibições de catálogo para o SQL Data Warehouse e Parallel Data Warehouse, consulte [SQL Data Warehouse e exibições do catálogo Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para criar um classificador de carga de trabalho, consulte [CLASSIFICADOR de carga de trabalho criar](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obter mais informações sobre a classificação de carga de trabalho, consulte o SQL Data Warehouse [carga de trabalho de classificação](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) e [importância da carga de trabalho](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
