---
description: sys.dm_hadr_auto_page_repair (Transact-SQL)
title: sys. dm_hadr_auto_page_repair (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 93c963fbe285407e56cafb8d13ebed0b7d4b3f31
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493679"
---
# <a name="sysdm_hadr_auto_page_repair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados de disponibilidade em uma réplica de disponibilidade hospedada para qualquer grupo de disponibilidade pela instância do servidor. Essa exibição contém linhas das últimas tentativas de reparo automático de página em um determinado banco de dados primário ou secundário, com um máximo de 100 linhas por banco de dados. Assim que o banco de dados atinge o máximo, a linha de sua próxima tentativa de conserto de página automático substitui uma das entradas existentes.
  
  A tabela a seguir define o significado das várias colunas:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados ao qual corresponde a linha.|  
|**file_id**|**int**|ID do arquivo em que a página está localizada.|  
|**page_id**|**bigint**|ID da página no arquivo.|  
|**error_type**|**int**|O tipo de erro. Os valores podem ser:<br /><br /> **-** 1 = todos os erros de hardware 823<br /><br /> 1 = 824 erros exceto uma soma de verificação inválida ou uma página interrompida (como uma ID de página inválida)<br /><br /> 2 = Soma de verificação inválida<br /><br /> 3 = Página interrompida|  
|**page_status**|**int**|O status da tentativa de conserto da página:<br /><br /> 2 = Enfileirada para solicitação do parceiro.<br /><br /> 3 = Solicitação enviada ao parceiro.<br /><br /> 4 = a página foi reparada com êxito.<br /><br /> 5 = a página não pôde ser reparada durante a última tentativa/reparo automático de página tentará reparar a página novamente.|  
|**modification_time**|**datetime**|Hora da última alteração no estado da página.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Reparo automático de página &#40;Grupos de Disponibilidade: Espelhamento de banco de dados&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [&#41;&#40;Transact-SQL de suspect_pages ](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

