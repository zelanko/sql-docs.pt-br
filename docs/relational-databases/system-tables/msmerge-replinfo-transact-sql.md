---
title: MSmerge_replinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5e7aab7d91bafcb79b7db8367011b36bd893e35d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_replinfo** tabela contém uma linha para cada assinatura. Essa tabela localiza informações sobre assinaturas. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|A ID exclusiva da replicação.|  
|**use_interactive_resolver**|**bit**|Especifica se o resolvedor interativo é usado durante a reconciliação.<br /><br /> **0** = não não usar o resolvedor interativo.<br /><br /> **1** = usar o resolvedor interativo.|  
|**validation_level**|**Int**|Tipo de validação para executar na assinatura. O nível de validação especificado pode ser um destes valores:<br /><br /> **0** não = nenhuma validação.<br /><br /> **1** = validação somente do número de linhas.<br /><br /> **2** = número de linhas e soma de verificação de validação.<br /><br /> **3** = número de linhas e soma de verificação binária.|  
|**resync_gen**|**bigint**|O número de geração usado para nova sincronização da assinatura. Um valor de **– 1** indica que a assinatura não está marcada para ser sincronizada novamente.|  
|**login_name**|**sysname**|O nome do usuário que criou a assinatura.|  
|**Nome do host**|**sysname**|O valor usado pelo filtro de linha com parâmetros ao gerar a partição para a assinatura.|  
|**merge_jobid**|**binary(16)**|A ID do trabalho de mesclagem para esta assinatura.|  
|**sync_info**|**Int**|Interno-somente para uso.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
