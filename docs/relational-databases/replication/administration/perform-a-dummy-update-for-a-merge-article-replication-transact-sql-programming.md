---
title: "Executar atualização fictícia para o artigo de mesclagem (programação T-SQL de replicação) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- sp_mergedummyupdate
- dummy updates [SQL Server replication]
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c3a30d3c0df0a3c73663aa7aee70360dd06f59d3
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>Executar uma atualização fictícia para um artigo de mesclagem (Programação Transact-SQL de replicação)
  As replicações de mesclagem usam gatilhos como parte do processo de replicação. Quando uma atualização é executada em uma tabela publicada, um gatilho de atualização é acionado. Em alguns casos, os dados podem ser atualizados sem que o gatilho seja acionado, como durante as operações WRITETEXT e UPDATETEXT. Nesses casos, você precisa adicionar uma instrução UPDATE fictícia explicitamente para replicar a alteração. Você pode adicionar uma instrução UPDATE fictícia que usa procedimentos armazenados de replicação.  
  
### <a name="to-add-a-dummy-update-statement"></a>Para adicionar uma instrução UPDATE fictícia  
  
1.  Execute a operação (por exemplo, UPDATETEXT) em uma linha em uma tabela de mesclagem publicada que exija uma atualização fictícia.  
  
2.  No servidor (Publicador ou Assinante) do banco de dados em que foi feita a alteração, execute [sp_mergedummyupdate &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md). Especifique a tabela onde as alterações foram feitas para o **@source_object**para o identificador exclusivo da linha alterada para **@rowguid**.  
  
3.  Sincronize a assinatura para replicar a linha alterada.  
  
  
