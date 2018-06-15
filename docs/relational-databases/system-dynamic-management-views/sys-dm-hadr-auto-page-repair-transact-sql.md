---
title: sys.dm_hadr_auto_page_repair (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 23c16b165148fc6e385474cbb3e0ef5cab920f5c
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34465372"
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados de disponibilidade em uma réplica de disponibilidade hospedada para qualquer grupo de disponibilidade pela instância do servidor. Essa exibição contém linhas das últimas tentativas de reparo automático de página em um determinado banco de dados primário ou secundário, com um máximo de 100 linhas por banco de dados. Assim que o banco de dados atinge o máximo, a linha de sua próxima tentativa de conserto de página automático substitui uma das entradas existentes.
  
  A tabela a seguir define o significado das diversas colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**Int**|ID do banco de dados ao qual corresponde a linha.|  
|**file_id**|**Int**|ID do arquivo em que a página está localizada.|  
|**page_id**|**bigint**|ID da página no arquivo.|  
|**error_type**|**Int**|O tipo de erro. Os valores podem ser:<br /><br /> **-** 1 = todos os erros de hardware 823<br /><br /> 1 = 824 erros que não seja uma soma de verificação inválida ou uma página interrompida (como uma ID de página inválida)<br /><br /> 2 = Soma de verificação inválida<br /><br /> 3 = Página interrompida|  
|**page_status**|**Int**|O status da tentativa de conserto da página:<br /><br /> 2 = Enfileirada para solicitação do parceiro.<br /><br /> 3 = Solicitação enviada ao parceiro.<br /><br /> 4 = Enfileirada para conserto de página automático (resposta recebida do parceiro).<br /><br /> 5 = Conserto de página automático efetuado com êxito; a página deve estar utilizável.<br /><br /> 6 = Irreparável. Isso indica que ocorreu um erro durante a tentativa do conserto da página, por exemplo, porque a página também está corrompida no parceiro, o parceiro está desconectado ou houve um problema de rede. Esse estado não é terminal; se o dano for encontrado novamente na página, a página será novamente solicitada ao parceiro.|  
|**modification_time**|**datetime**|Hora da última alteração no estado da página.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Reparo automático de página &#40;Grupos de disponibilidade: espelhamento de banco de dados&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages & #40; Transact-SQL & #41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

