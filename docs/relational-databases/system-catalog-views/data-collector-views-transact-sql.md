---
title: Exibições do coletor de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- data collector [SQL Server], views
ms.assetid: a005e885-7813-4c7e-b332-b01d9e9d4054
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9e412f796a5b04f980557b5a3131763811aa78da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68033171"
---
# <a name="data-collector-views-transact-sql"></a>Exibições do Coletor de Dados (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O coletor de dados oferece as exibições a seguir, com informações sobre a configuração do coletor de dados, como propriedades do tipo de coletor, conjuntos de coleta e itens de conjunto de coleta, assim como estatísticas de execução obtidas quando um conjunto de coleta é executado. Essas exibições, que estão no banco de dados **msdb** , também fornecem uma camada de abstração para as tabelas subjacentes. Essa abstração aprimora a segurança ao impedir o acesso direto às tabelas, enquanto permite alterações nas mesmas, sem que os aplicativos associados sejam afetados.  
  
|||  
|-|-|  
|[&#41;&#40;Transact-SQL de syscollector_collection_items](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|[&#41;&#40;Transact-SQL de syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|  
|[&#41;&#40;Transact-SQL de syscollector_collector_types](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|[&#41;&#40;Transact-SQL de syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|  
|[&#41;&#40;Transact-SQL de syscollector_execution_log](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|[&#41;&#40;Transact-SQL de syscollector_execution_log_full](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|  
|[&#41;&#40;Transact-SQL de syscollector_execution_stats](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)||  
  
## <a name="see-also"></a>Consulte Também  
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
