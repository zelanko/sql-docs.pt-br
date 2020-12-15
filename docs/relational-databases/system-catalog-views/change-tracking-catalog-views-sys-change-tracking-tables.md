---
description: Exibições de catálogo Controle de Alterações-sys.change_tracking_tables
title: sys.change_tracking_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1837ce515f31a0a8c98c2c63b0ef4ab853bad19a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475237"
---
# <a name="change-tracking-catalog-views---syschange_tracking_tables"></a>Exibições de catálogo Controle de Alterações-sys.change_tracking_tables
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada tabela do banco de dados atual que tiver o controle de alterações habilitado.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID de uma tabela que tem um diário de alteração. A tabela poderá ter um diário de alteração mesmo se o controle de alterações estiver desabilitado no momento.<br /><br /> A ID da tabela é exclusiva no banco de dados.|  
|is_track_columns_updated_on|**bit**|Estado atual do controle de alterações na tabela:<br /><br /> 0 = OFF<br /><br /> 1 = ON|  
|begin_version|**bigint**|Versão do banco de dados quando foi iniciado o controle de alterações para a tabela. Essa versão em geral indica quando o controle de alterações está habilitado, mas esse valor será redefinido se a tabela estiver truncada.|  
|cleanup_version|**bigint**|Versão superior em que a limpeza deveria ter removido as informações de controle de alterações.|  
|min_valid_version|**bigint**|Versão válida mínima de informações de controle de alterações disponíveis para a tabela.<br /><br /> Na obtenção de alterações de uma tabela associada a essa linha, o valor de last_sync_version deverá ser maior que ou igual ao da versão informada por esta coluna. Para obter mais informações, consulte [CHANGE_TRACKING_MIN_VALID_VERSION &#40;&#41;Transact-SQL ](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md).|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Controle de Alterações exibições de catálogo &#40;Transact-SQL&#41;](./catalog-views-transact-sql.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
