---
description: '&lt;esquema &gt; de conflict_ _ &lt; tabela &gt; (Transact-SQL)'
title: '&lt;esquema &gt; de conflict_ _ &lt; tabela &gt; (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/15/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 126474b4efe2eafb5c235d1ba4a31e433d71500c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544643"
---
# <a name="conflict_ltschemagt_lttablegt-transact-sql"></a>&lt;esquema &gt; de conflict_ _ &lt; tabela &gt; (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A \<schema> tabela conflict_ _ \<table> contém informações sobre linhas conflitantes na replicação ponto a ponto. Existe uma tabela de conflitos para cada tabela replicada na publicação, onde o nome da tabela de conflitos é anexada ao nome da publicação e do esquema. Estas tabelas de conflitos específicas do artigo existem em cada banco de dados de publicação.  
  
 Para replicação ponto a ponto, por padrão, o Distribution Agent falha ao detectar um conflito. Um erro de conflito é registrado no log de erros, mas nenhum dado de conflito é registrado na tabela de conflito; assim, não está disponível para exibição. Se o Distribution Agent tiver permissão para continuar, um conflito será registrado localmente em cada nó onde ele for detectado. Para obter mais informações, consulte “Controlando conflitos” em [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|__$originator_id|**int**|ID do nó no qual originou-se a alteração conflitante. Para obter uma lista de IDs, execute [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).|  
|__$origin_datasource|**int**|Nó no qual originou-se a alteração conflitante.|  
|__$tranid|**nvarchar (40)**|LSN (Número de Sequência de Log) da alteração conflitante quando ela foi aplicada no __$origin_datasource.|  
|__$conflict_type|**int**|O tipo de conflito, que pode ser um dos seguintes valores:<br /><br /> 1: uma atualização falhou porque a linha local foi alterada por outra atualização ou excluída e, depois, reinserida.<br /><br /> 2: uma atualização falhou porque a linha local já foi excluída.<br /><br /> 3: uma exclusão falhou porque a linha local foi alterada por outra atualização ou excluída e, depois, reinserida.<br /><br /> 4: uma exclusão falhou porque a linha local já foi excluída.<br /><br /> 5: uma inserção falhou porque a linha local já foi inserida ou foi inserida e, depois, atualizada.|  
|__$is_winner|**bit**|Indica se a linha nesta tabela foi a vencedora do conflito, o que significa que ela foi aplicada no nó local.|  
|__$pre_version|**varbinary (32)**|Versão do banco de dados no qual originou-se a alteração conflitante.|  
|__$reason_code|**int**|Código de resolução para o conflito. Pode ser um dos seguintes valores:<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> Para obter mais informações, confira **_ $ reason_text**.|  
|__$reason_text|**nvarchar (720)**|Resolução para o conflito. Pode ser um dos seguintes valores:<br /><br /> Resolvido (1)<br /><br /> Não resolvido (2)<br /><br /> Desconhecido (0)|  
|__$update_bitmap|**varbinary (** *n* **)**. O tamanho varia dependendo do conteúdo.|Bitmap que indica quais colunas foram atualizadas na ocorrência de um conflito atualização- atualização.|  
|__$inserted_date|**datetime**|Dada e hora em que a linha conflitante foi inserida nesta tabela.|  
|__$row_id|**timestamp**|Versão da linha associada à linha que causou o conflito.|  
|__$change_id|**binário (8)**|No caso de uma linha local, este valor é igual a __$row_id da linha de entrada que gerou o conflito com a linha local. Esse valor é NULL para uma linha de entrada.|  
|\<base table column names>|\<base table column types>|A tabela de conflito contém uma coluna para cada coluna na tabela base.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
