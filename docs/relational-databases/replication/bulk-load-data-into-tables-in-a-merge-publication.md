---
title: Carregar dados em massa em tabelas em uma publicação de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfc47282eecfa121015298d5561c5e39fbc872ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>Carregar dados em massa em tabelas em uma publicação de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando os dados são carregados em tabelas com o comando [bcp Utility](../../tools/bcp-utility.md) ou [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) , por padrão, os gatilhos da replicação de mesclagem que mantêm dados de rastreamento na tabela de sistema [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) não são acionados. Você pode forçar os gatilhos de replicação de mesclagem para serem acionados enquanto os dados forem carregados ou, você pode inserir os metadados de replicação gerados programaticamente após a operação de cópia em massa usando os procedimentos armazenados de replicação.  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>Para carregar dados em massa em tabelas publicadas por replicação de mesclagem usando o utilitário bcp  
  
1.  No Publicador ou no Assinante, execute [bcp Utility](../../tools/bcp-utility.md) ou [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) para inserir dados em uma tabela publicada usando a replicação de mesclagem.  
  
2.  Use um dos métodos abaixo para assegurar que são gerados os metadados de replicação para os dados inseridos.  
  
    -   Execute a cópia em massa usando a opção FIRE_TRIGGERS.  
  
    -   No banco de dados no qual os dados foram inseridos, execute [sp_addtabletocontents &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md). Especifique o nome da tabela na qual os dados foram inseridos para **@table_name**.  
  
  
