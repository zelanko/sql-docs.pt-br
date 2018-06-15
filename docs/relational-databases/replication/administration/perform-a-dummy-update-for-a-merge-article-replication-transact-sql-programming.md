---
title: Executar atualização fictícia para o artigo de mesclagem (programação T-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_mergedummyupdate
- dummy updates [SQL Server replication]
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eea3359fa0c0d3cbf91621277ce2737bbb5fc60b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32952911"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>Executar uma atualização fictícia para um artigo de mesclagem (Programação Transact-SQL de replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  As replicações de mesclagem usam gatilhos como parte do processo de replicação. Quando uma atualização é executada em uma tabela publicada, um gatilho de atualização é acionado. Em alguns casos, os dados podem ser atualizados sem que o gatilho seja acionado, como durante as operações WRITETEXT e UPDATETEXT. Nesses casos, você precisa adicionar uma instrução UPDATE fictícia explicitamente para replicar a alteração. Você pode adicionar uma instrução UPDATE fictícia que usa procedimentos armazenados de replicação.  
  
### <a name="to-add-a-dummy-update-statement"></a>Para adicionar uma instrução UPDATE fictícia  
  
1.  Execute a operação (por exemplo, UPDATETEXT) em uma linha em uma tabela de mesclagem publicada que exija uma atualização fictícia.  
  
2.  No servidor (Publicador ou Assinante) do banco de dados em que foi feita a alteração, execute [sp_mergedummyupdate &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md). Especifique a tabela onde as alterações foram feitas para o **@source_object**para o identificador exclusivo da linha alterada para **@rowguid**.  
  
3.  Sincronize a assinatura para replicar a linha alterada.  
  
  
