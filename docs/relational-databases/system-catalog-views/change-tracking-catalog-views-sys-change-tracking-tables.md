---
title: change_tracking_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- change_tracking_tables_TSQL
- sys.change_tracking_tables
- change_tracking_tables
- sys.change_tracking_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], sys.change_tracking_tables
- sys.change_tracking_tables
ms.assetid: 97ec69b6-0d49-4d98-82f0-d3e77ba1ad2b
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1e4447f994fa13277892243befa8264bbafe3d13
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="change-tracking-catalog-views---syschangetrackingtables"></a>Alterar modos de exibição de catálogo de controle - change_tracking_tables
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada tabela do banco de dados atual que tiver o controle de alterações habilitado.  
   
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_id|**Int**|ID de uma tabela que tem um diário de alteração. A tabela poderá ter um diário de alteração mesmo se o controle de alterações estiver desabilitado no momento.<br /><br /> A ID da tabela é exclusiva no banco de dados.|  
|is_track_columns_updated_on|**bit**|Estado atual do controle de alterações na tabela:<br /><br /> 0 = OFF<br /><br /> 1 = ON|  
|begin_version|**bigint**|Versão do banco de dados quando foi iniciado o controle de alterações para a tabela. Essa versão em geral indica quando o controle de alterações está habilitado, mas esse valor será redefinido se a tabela estiver truncada.|  
|cleanup_version|**bigint**|Versão superior em que a limpeza deveria ter removido as informações de controle de alterações.|  
|min_valid_version|**bigint**|Versão válida mínima de informações de controle de alterações disponíveis para a tabela.<br /><br /> Na obtenção de alterações de uma tabela associada a essa linha, o valor de last_sync_version deverá ser maior que ou igual ao da versão informada por esta coluna. Para obter mais informações, consulte [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md).|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Exibições do catálogo de controle de alterações &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
