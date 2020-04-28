---
title: MSpublisher_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
author: stevestein
ms.author: sstein
ms.openlocfilehash: da208c7fb83053c1817693bb16d16c3488fe90c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68032611"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSpublisher_databases** contém uma linha para cada par de banco de dados Publicador/Publicador atendido pelo distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|A ID do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**id**|**int**|A ID da linha.|  
|**publisher_engine_edition**|**int**|A versão do Publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que pode ser uma das seguintes:<br /><br /> **10** = edição pessoal<br /><br /> **11** = mecanismo de área de trabalho (MSDE)<br /><br /> **20** = padrão<br /><br /> **21** = grupo de trabalho<br /><br /> **30** = Enterprise (avaliação)<br /><br /> **31** = desenvolvedor<br /><br /> **40** = Express (Express não pode ser um Publicador. Esse valor está presente para integridade.)|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
