---
title: MSmerge_settingshistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9ac532e5212f32e5ee3bda029a2a7fb5a1231974
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829220"
---
# <a name="msmerge_settingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSmerge_settingshistory** é usada para manter um histórico das alterações feitas nas propriedades do artigo e da publicação para replicação de mesclagem, com uma linha para cada alteração feita em uma topologia de replicação de mesclagem. Essa tabela também armazena informações sobre quando as configurações de propriedade iniciais foram feitas. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**EventTime**|**datetime**|A data e hora em que o evento ocorreu.|  
|**pubid**|**uniqueidentifier**|O número de identificação exclusivo de determinada publicação.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**EventType**|**tinyint**|Especifica o tipo de evento que está sendo registrado, que pode ser um dos seguintes:<br /><br /> **1** -configuração de propriedade de nível de publicação inicial.<br /><br /> **2** -alterar em uma propriedade de publicação.<br /><br /> **101** -configuração da Propriedade do artigo inicial.<br /><br /> **102** -alterar em uma propriedade de artigo.|  
|**propertyname**|**sysname**|O nome da propriedade definida ou alterada|  
|**previousvalue**|**sysname**|O valor da propriedade anterior se uma propriedade tiver sido alterada.|  
|**NewValue**|**sysname**|O valor para o qual a propriedade foi alterada ou no qual ela foi criada.|  
|**eventtext**|**nvarchar (2000)**|A cadeia de caracteres que descreve o evento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
