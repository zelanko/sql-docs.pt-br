---
title: pdw_diag_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a61d85c607824420f69c48fa1a84e5d8435a1f85
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662754"
---
# <a name="syspdwdiagsessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre as várias sessões de diagnóstico que foram criados no sistema.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|Nome da sessão de diagnóstico.<br /><br /> A chave para este modo de exibição.||  
|**xml_data**|**nvarchar(4000)**|Carga XML que descreve a sessão.||  
|**is_active**|**bit**|Sinalizador que indica se o sinalizador está ativo.||  
|**host_address**|**nvarchar(255)**|Endereço do computador que hospeda a definição de sessão (nó de controle).||  
|**principal_id**|**int**|ID do usuário que criou a sessão no nível do banco de dados.||  
|**database_id**|**int**|ID do banco de dados que é o escopo da sessão de diagnóstico.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
