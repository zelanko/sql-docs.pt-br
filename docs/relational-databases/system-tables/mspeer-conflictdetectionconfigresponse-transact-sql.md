---
title: MSpeer_conflictdetectionconfigresponse (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 430008b1a689c413bf69c9907a60f4129dc8e5b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006879"
---
# <a name="mspeerconflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado em replicação ponto a ponto para armazenar a resposta de cada nó para solicitação de configuração de toda a topologia. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|request_id|**int**|Identifica uma entrada de solicitação de configuração de conflito na [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md) tabela.|  
|peer_node|**sysname**|O nome do instância do servidor que gerou a resposta.|  
|peer_db|**sysname**|Banco de dados de assinatura no nível que gerou a resposta.|  
|peer_version|**sysname**|Identifica o número da versão do Publicador.|  
|peer_db_version|**sysname**|Identifica o número da versão do banco de dados de nível.|  
|is_peer|**bit**|Indica se um nó é um Assinante somente leitura. Um valor de **0** indicou um assinante somente leitura.|  
|conflict_detection_enabled|**bit**|Indica se detecção de conflito está ativada para a topologia.|  
|originator_id|**varbinary(16)**|Identifica cada nó na topologia com a finalidade de detecção de conflito. Para obter mais informações, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**int**|Período de tempo, em dias, que os metadados são armazenados em tabelas de conflitos.|  
|peer_subscriptions|**XML**|Informações sobre o nó que respondeu à solicitação.|  
|progress_phase|**nvarchar(32)**|Identifica a fase atual de processamento, usando um dos seguintes valores:<br /><br /> Started (iniciado)<br /><br /> Versão de nível coletada<br /><br /> Status coletado|  
|modified_date|**datetime**|Data e hora em que uma fase foi concluída.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
