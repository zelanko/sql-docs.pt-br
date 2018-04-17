---
title: Conflict _&lt;esquema&gt;_&lt;tabela&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2016
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
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9c5faa805785b856aca59ff2cd026b6ee9cf5c0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="conflictltschemagtlttablegt-transact-sql"></a>Conflict _&lt;esquema&gt;_&lt;tabela&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O Conflict _\<esquema > _\<tabela > tabela contém informações sobre linhas conflitantes na replicação ponto a ponto. Existe uma tabela de conflitos para cada tabela replicada na publicação, onde o nome da tabela de conflitos é anexada ao nome da publicação e do esquema. Estas tabelas de conflitos específicas do artigo existem em cada banco de dados de publicação.  
  
 Para replicação ponto a ponto, por padrão, o Distribution Agent falha ao detectar um conflito. Um erro de conflito é registrado no log de erros, mas nenhum dado de conflito é registrado na tabela de conflito; assim, não está disponível para exibição. Se o Distribution Agent tiver permissão para continuar, um conflito será registrado localmente em cada nó onde ele for detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|__$originator_id|**Int**|ID do nó no qual originou-se a alteração conflitante. Para obter uma lista de IDs, execute [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).|  
|__$origin_datasource|**Int**|Nó no qual originou-se a alteração conflitante.|  
|__$tranid|**nvarchar (40)**|LSN (Número de Sequência de Log) da alteração conflitante quando ela foi aplicada no __$origin_datasource.|  
|__$conflict_type|**Int**|O tipo de conflito, que pode ser um dos seguintes valores:<br /><br /> 1: uma atualização falhou porque a linha local foi alterada por outra atualização ou excluída e, depois, reinserida.<br /><br /> 2: uma atualização falhou porque a linha local já foi excluída.<br /><br /> 3: uma exclusão falhou porque a linha local foi alterada por outra atualização ou excluída e, depois, reinserida.<br /><br /> 4: uma exclusão falhou porque a linha local já foi excluída.<br /><br /> 5: uma inserção falhou porque a linha local já foi inserida ou foi inserida e, depois, atualizada.|  
|__$is_winner|**bit**|Indica se a linha nesta tabela foi a vencedora do conflito, o que significa que ela foi aplicada no nó local.|  
|__$pre_version|**varbinary (32)**|Versão do banco de dados no qual originou-se a alteração conflitante.|  
|__$reason_code|**Int**|Código de resolução para o conflito. Pode ser um dos seguintes valores:<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> Para obter mais informações, consulte **_ $reason_text**.|  
|__$reason_text|**nvarchar (720)**|Resolução para o conflito. Pode ser um dos seguintes valores:<br /><br /> Resolvido (1)<br /><br /> Não resolvido (2)<br /><br /> Desconhecido (0)|  
|__$update_bitmap|**varbinary (** *n* **)**. Tamanho varia de acordo com o conteúdo.|Bitmap que indica quais colunas foram atualizadas na ocorrência de um conflito atualização- atualização.|  
|__$inserted_date|**datetime**|Dada e hora em que a linha conflitante foi inserida nesta tabela.|  
|__$row_id|**timestamp**|Versão da linha associada à linha que causou o conflito.|  
|__$change_id|**binary (8)**|No caso de uma linha local, este valor é igual a __$row_id da linha de entrada que gerou o conflito com a linha local. Esse valor é NULL para uma linha de entrada.|  
|\<nomes de coluna da tabela de base >|\<tipos de coluna de tabela base >|A tabela de conflito contém uma coluna para cada coluna na tabela base.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
