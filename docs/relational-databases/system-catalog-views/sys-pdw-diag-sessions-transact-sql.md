---
title: sys. pdw_diag_sessions (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: fa06005679e31381f723b30b9f68e5ce0d89ae1e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127685"
---
# <a name="syspdw_diag_sessions-transact-sql"></a>sys. pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contém informações sobre as várias sessões de diagnóstico que foram criadas no sistema.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar (255)**|Nome da sessão de diagnóstico.<br /><br /> Chave para esta exibição.||  
|**xml_data**|**nvarchar(4000)**|Carga XML que descreve a sessão.||  
|**is_active**|**bit**|Sinalizador que indica se o sinalizador está ativo.||  
|**host_address**|**nvarchar (255)**|Endereço do computador que hospeda a definição de sessão (nó de controle).||  
|**principal_id**|**int**|ID do usuário que criou a sessão no nível do banco de dados.||  
|**database_id**|**int**|ID do banco de dados que é o escopo da sessão de diagnóstico.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
