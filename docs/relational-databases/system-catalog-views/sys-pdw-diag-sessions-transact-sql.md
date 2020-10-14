---
description: sys.pdw_diag_sessions (Transact-SQL)
title: sys.pdw_diag_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e8fade6ec60ada411ee78027d01f9616e499f755
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036735"
---
# <a name="syspdw_diag_sessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contém informações sobre as várias sessões de diagnóstico que foram criadas no sistema.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|Nome da sessão de diagnóstico.<br /><br /> Chave para esta exibição.||  
|**xml_data**|**nvarchar(4000)**|Carga XML que descreve a sessão.||  
|**is_active**|**bit**|Sinalizador que indica se o sinalizador está ativo.||  
|**host_address**|**nvarchar(255)**|Endereço do computador que hospeda a definição de sessão (nó de controle).||  
|**principal_id**|**int**|ID do usuário que criou a sessão no nível do banco de dados.||  
|**database_id**|**int**|ID do banco de dados que é o escopo da sessão de diagnóstico.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
