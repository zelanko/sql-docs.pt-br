---
title: MSmerge_genhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bee379b36d0af531ee6a5d3d3b6b129199cec46c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005103"
---
# <a name="msmergegenhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_genhistory** tabela contém uma linha para cada geração que um assinante conhece (dentro do período de retenção). Ela é usada para evitar enviar gerações comuns durante trocas e para sincronizar novamente Assinantes restaurados de backups. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|O identificador global das alterações identificadas pela geração no Assinante.|  
|**pubid**|**uniqueidentifier**|O identificador da publicação.|  
|**Geração**|**bigint**|O valor de geração.|  
|**art_nick**|**Int**|O apelido do artigo.|  
|**Apelidos**|**varbinary(1001)**|Uma lista de apelidos de outros Assinantes que já têm essa geração. É usado para evitar enviar uma geração a um Assinante que já viu essas alterações. Apelidos da lista de apelidos são mantidos em ordem classificada para tornar as pesquisas mais eficientes. Se houver mais apelidos do que o que cabe nesse campo, eles não se beneficiarão dessa otimização.|  
|**coldate**|**datetime**|Data em que a geração atual é adicionada à tabela.|  
|**genstatus**|**tinyint**|O status da geração como segue:<br /><br /> **0** = aberto.<br /><br /> **1** = fechado.<br /><br /> **2** = fechado e originado em outro assinante.|  
|**changecount**|**Int**|O número de alterações refletido em uma determinada geração|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
