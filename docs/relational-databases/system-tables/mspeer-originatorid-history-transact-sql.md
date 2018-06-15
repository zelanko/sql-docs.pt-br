---
title: MSpeer_originatorid_history (Transact-SQL) | Microsoft Docs
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
- MSpeer_originatorid_history_TSQL
- MSpeer_originatorid_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_originatorid_history
ms.assetid: c1f53d0f-4080-43ff-be38-2b10395c68c9
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 145392c2ff7ebb3685a9ce710678ab88639d2842
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005093"
---
# <a name="mspeeroriginatoridhistory-transact-sql"></a>MSpeer_originatorid_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada ID de originador que foi definida na topologia. Isso inclui ID para nós que são não estão mais ativos. A tabela é usada ao configurar um novo nó para a detecção de conflito, a fim de assegurar que a ID de originador especificada não esteja sendo usada. Essa tabela é armazenada no banco de dados de publicação. Para obter mais informações sobre a detecção de conflitos, consulte [detecção de conflito na replicação ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|originator_publication|**sysname**|Publicação para a qual a ID de originador foi especificada.|  
|originator_id|**Int**|Número que identifica cada nó na topologia com a finalidade de detecção de conflito.|  
|originator_node|**sysname**|Instância do servidor para a qual a ID de originador foi especificada.|  
|originator_db|**sysname**|Banco de dados da publicação para o qual a ID de originador foi especificada.|  
|originator_db_version|**Int**|Identifica o número da versão do banco de dados de origem.|  
|originator_version|**Int**|Identifica o número da versão do Publicador.|  
|inserted_date|**datetime**|Data e hora em que a linha para a ID do originador foi inserida nesta tabela.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
