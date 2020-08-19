---
description: MScached_peer_lsns (Transact-SQL)
title: MScached_peer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5c84f47e733937baa9ac01f99270a6759747d4c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446545"
---
# <a name="mscached_peer_lsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MScached_peer_lsns** é usada para rastrear os valores LSN no log de transações que são usados para determinar quais comandos retornar a um determinado Assinante na replicação ponto a ponto. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|A ID do Distribution Agent.|  
|**autor**|**sysname**|O nome do Publicador de origem.|  
|**originator_db**|**sysname**|O nome do banco de dados de publicação de origem.|  
|**originator_publication_id**|**int**|Identifica a publicação de origem.|  
|**originator_db_version**|**int**|Identifica o número da versão do banco de dados de origem.|  
|**originator_lsn**|**varbinary(16)**|O LSN da transação de origem.|  
  
## <a name="remarks"></a>Comentários  
 Valores LSN só são usados imediatamente após a inserção e não têm nenhum significado duradouro no sistema.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
