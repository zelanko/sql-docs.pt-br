---
title: sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
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
ms.openlocfilehash: 9afd00a887244c02849d40eed635500b06533709
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582719"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (Transact-SQL) (Preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

> [!Note]
> Classificação de carga de trabalho está disponível para visualização no SQL Data Warehouse Gen2. Visualização de classificação de gerenciamento de carga de trabalho e a importância é para compilações com uma data de lançamento do dia 9 de abril de 2019 ou posterior.  Os usuários devem evitar usando builds anteriores a essa data para gerenciamento de carga de trabalho de teste.  Para determinar se a compilação for com capacidade de gerenciamento de carga de trabalho, execute select @@version quando conectado à instância do SQL Data Warehouse.

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
