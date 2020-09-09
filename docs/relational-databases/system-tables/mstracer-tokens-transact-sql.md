---
description: MStracer_tokens (Transact-SQL)
title: MStracer_tokens (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MStracer_tokens_TSQL
- MStracer_tokens
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_tokens system table
ms.assetid: b273aa48-8188-4213-8e2c-311543c3236f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c004c7a578e1fd2a21cd44f8149d2f850dec8d1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547029"
---
# <a name="mstracer_tokens-transact-sql"></a>MStracer_tokens (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MStracer_tokens** mantém um registro de registros de token de rastreamento inseridos em uma publicação. Essa tabela é armazenada no banco de dados de distribuição e é usada pela replicação para monitorar o desempenho.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**trace_id**|**int**|Identifica um registro de token de rastreamento.|  
|**publication_id**|**int**|Identifica a publicação na qual o registro de token de rastreamento foi inserido.|  
|**publisher_commit**|**datetime**|A data e hora em que o registro de token de rastreamento foi confirmado no Publicador.|  
|**distributor_commit**|**datetime**|A data e hora em que o registro de token de rastreamento foi confirmado no Distribuidor.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
