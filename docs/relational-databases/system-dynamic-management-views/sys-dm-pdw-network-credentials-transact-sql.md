---
description: sys.dm_pdw_network_credentials (Transact-SQL)
title: sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 243319d55d703317847dd1475398b23bea56afc6
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035325"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Retorna uma lista de todas as credenciais de rede armazenadas no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo para todos os servidores de destino. Os resultados são listados para o nó de controle e para cada nó de computação.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|ID numérica exclusiva associada ao nó.|  
|target_server_name|**nvarchar(32)**|Endereço IP do servidor de destino que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] será acessado usando as credenciais de nome de usuário e senha.|  
|Nome de Usuário|**nvarchar(32)**|Nome de usuário para o qual a senha é armazenada.|  
|last_modified|**datetime**|DateTime da última operação que modificou a credencial.|  
  
## <a name="permissions"></a>Permissões  
 Requer o estado do servidor de exibição.  
  
## <a name="general-remarks"></a>Comentários gerais  
 A chave para essa exibição de gerenciamento dinâmico é *pdw_node_id* mais *target_server_name*.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
