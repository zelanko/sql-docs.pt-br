---
title: MSmerge_settingshistory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac25c834da1e4101d7a5ae9f58f479994fd0e1b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msmergesettingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_settingshistory** tabela é usada para manter um histórico das alterações feitas às propriedades de artigo e publicação para replicação de mesclagem, com uma linha para cada alteração feita em uma topologia de replicação de mesclagem. Essa tabela também armazena informações sobre quando as configurações de propriedade iniciais foram feitas. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|A data e hora em que o evento ocorreu.|  
|**PubID**|**uniqueidentifier**|O número de identificação exclusivo de determinada publicação.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**EventType**|**tinyint**|Especifica o tipo de evento que está sendo registrado, que pode ser um dos seguintes:<br /><br /> **1** – configuração de propriedade de nível de publicação inicial.<br /><br /> **2** -alteração em uma propriedade de publicação.<br /><br /> **101** -configuração de propriedade de artigo inicial.<br /><br /> **102** -alteração na propriedade do artigo.|  
|**PropertyName**|**sysname**|O nome da propriedade definida ou alterada|  
|**previousvalue**|**sysname**|O valor da propriedade anterior se uma propriedade tiver sido alterada.|  
|**NewValue**|**sysname**|O valor para o qual a propriedade foi alterada ou no qual ela foi criada.|  
|**eventText**|**nvarchar(2000)**|A cadeia de caracteres que descreve o evento.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
