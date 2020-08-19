---
description: MSpeer_originatorid_history (Transact-SQL)
title: MSpeer_originatorid_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_originatorid_history_TSQL
- MSpeer_originatorid_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_originatorid_history
ms.assetid: c1f53d0f-4080-43ff-be38-2b10395c68c9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 957ec6b764e18043aab4d68acff4db056cefb2fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469020"
---
# <a name="mspeer_originatorid_history-transact-sql"></a>MSpeer_originatorid_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada ID de originador que foi definida na topologia. Isso inclui ID para nós que são não estão mais ativos. A tabela é usada ao configurar um novo nó para a detecção de conflito, a fim de assegurar que a ID de originador especificada não esteja sendo usada. Essa tabela é armazenada no banco de dados de publicação. Para obter mais informações sobre a detecção de conflitos, consulte [detecção de conflitos na replicação ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|originator_publication|**sysname**|Publicação para a qual a ID de originador foi especificada.|  
|originator_id|**int**|Número que identifica cada nó na topologia com a finalidade de detecção de conflito.|  
|originator_node|**sysname**|Instância do servidor para a qual a ID de originador foi especificada.|  
|originator_db|**sysname**|Banco de dados da publicação para o qual a ID de originador foi especificada.|  
|originator_db_version|**int**|Identifica o número da versão do banco de dados de origem.|  
|originator_version|**int**|Identifica o número da versão do Publicador.|  
|inserted_date|**datetime**|Data e hora em que a linha para a ID do originador foi inserida nesta tabela.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
