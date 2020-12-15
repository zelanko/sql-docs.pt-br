---
description: sys.workload_management_workload_classifiers (Transact-SQL)
title: sys.workload_management_workload_classifiers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest
ms.openlocfilehash: 6d1bb241923146454d63cb5a1bd0c8463e81fb00
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477297"
---
# <a name="sysworkload_management_workload_classifiers-transact-sql"></a>sys.workload_management_workload_classifiers (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

 Retorna detalhes para classificadores de carga de trabalho.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID exclusiva do classificador. Não permite valor nulo||
group_name|**sysname**|Nome do grupo de carga de trabalho ao qual o classificador está atribuído. Não permite valor nulo. Junção para sys.workload_management_workload_groups ||
name|**sysname**|Nome do classificador. Deve ser exclusivo para a instância. Não permite valor nulo.||
|importance|**sysname**|É a importância relativa de uma solicitação neste grupo de carga de trabalho e entre grupos de carga de trabalho para recursos compartilhados.  A importância especificada no classificador substitui a configuração de importância do grupo de carga de trabalho. Permite valor nulo.  Quando NULL, a configuração de importância do grupo de carga de trabalho é usada.|baixa, below_normal, normal (padrão), above_normal, alta |
|create_time|**datetime**|Hora em que o classificador foi criado. Não permite valor nulo.||
modify_time|**datetime**|Hora em que o classificador foi modificado pela última vez. Não permite valor nulo.||
is_enabled|**bit**|INTERNAL||
|&nbsp;||||
  
## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.

## <a name="next-steps"></a>Próximas etapas

 Para obter uma lista de todas as exibições de catálogo para o Azure Synapse Analytics e Parallel data warehouse, consulte [Azure Synapse Analytics e exibições do catálogo de data warehouse paralela](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para criar um classificador de carga de trabalho, consulte [criar classificação de carga de trabalho](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obter mais informações sobre a classificação de carga de trabalho, consulte [classificação de carga de trabalho](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
