---
title: MSmerge_settingshistory (Transact-SQL) | Microsoft Docs
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
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2bb8007d97619b3cbe7302fbf00bcfd98584539e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="msmergesettingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_settingshistory** tabela é usada para manter um histórico das alterações feitas às propriedades de artigo e publicação para replicação de mesclagem, com uma linha para cada alteração feita em uma topologia de replicação de mesclagem. Essa tabela também armazena informações sobre quando as configurações de propriedade iniciais foram feitas. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|A data e hora em que o evento ocorreu.|  
|**pubid**|**uniqueidentifier**|O número de identificação exclusivo de determinada publicação.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**EventType**|**tinyint**|Especifica o tipo de evento que está sendo registrado, que pode ser um dos seguintes:<br /><br /> **1** – configuração de propriedade de nível de publicação inicial.<br /><br /> **2** -alteração em uma propriedade de publicação.<br /><br /> **101** -configuração de propriedade de artigo inicial.<br /><br /> **102** -alteração na propriedade do artigo.|  
|**propertyname**|**sysname**|O nome da propriedade definida ou alterada|  
|**previousvalue**|**sysname**|O valor da propriedade anterior se uma propriedade tiver sido alterada.|  
|**NewValue**|**sysname**|O valor para o qual a propriedade foi alterada ou no qual ela foi criada.|  
|**eventText**|**nvarchar(2000)**|A cadeia de caracteres que descreve o evento.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
