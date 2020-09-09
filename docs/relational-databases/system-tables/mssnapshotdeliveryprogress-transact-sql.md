---
description: MSsnapshotdeliveryprogress (Transact-SQL)
title: MSsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 733f82a23c61d41691c3845b2482a0aa0c3c2bcc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540195"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSsnapshotdeliveryprogress** é usada para controlar os arquivos que foram entregues com êxito ao Assinante quando um instantâneo está sendo aplicado. Esses dados são usados para retomar a entrega de arquivos quando o Merge Agent não consegue entregar todos os arquivos durante a sessão, para que os mesmos arquivos não sejam entregues novamente na próxima execução do Merge Agent. Essa tabela é armazenada no Assinante, no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifica o caminho para a pasta de instantâneo na qual o arquivo foi entregue com êxito. Para publicações que usam filtros com parâmetros, a cadeia de caracteres **dynsnap** será anexada ao valor.|  
|**progress_token_hash**|**int**|Um valor de hash gerado com base no valor de *progress_token* que é usado para melhorar a eficiência da pesquisa para um determinado valor de *progress_token* .|  
|**progress_token**|**nvarchar (500)**|Identifica um valor entregue com êxito, onde o valor é uma combinação do nome de arquivo e caminho.|  
|**progress_timestamp**|**datetime**|O valor de **data e hora** que indica quando um arquivo de instantâneo foi entregue com êxito.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
