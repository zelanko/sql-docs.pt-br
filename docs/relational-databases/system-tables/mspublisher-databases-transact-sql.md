---
title: MSpublisher_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 130a176655a7574903e85aa6cfa55037ca977448
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mspublisherdatabases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSpublisher_databases** tabela contém uma linha para cada par de banco de dados publicador/publicador servido pelo distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**id**|**Int**|A ID da linha.|  
|**publisher_engine_edition**|**Int**|A versão do Publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que pode ser uma das seguintes:<br /><br /> **10** = personal Edition<br /><br /> **11** = desktop Engine (MSDE)<br /><br /> **20** = padrão<br /><br /> **21** = grupo de trabalho<br /><br /> **30** = Enterprise (avaliação)<br /><br /> **31** = developer<br /><br /> **40** = express (Express não pode ser um publicador. Esse valor está presente para integridade.)|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
