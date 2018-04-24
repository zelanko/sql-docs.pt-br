---
title: MSSQL_REPL020011 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_REPL020011 error
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2eb3157c9994909c9473921fc4b4f66ada98c7ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlrepl020011"></a>MSSQL_REPL020011
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20011|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O processo não pôde executar '%1' em '%2'.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro pode ser acionado em várias circunstâncias durante o processamento da replicação transacional, como quando o Agente de Leitor de Log executa **sp_replcmds** (O processo não pôde executar 'sp_replcmds' em \<ServerName>) ou **sp_repldone** (O processo não pôde executar 'sp_repldone' em \<ServerName>).  
  
## <a name="user-action"></a>Ação do usuário  
 Se o erro for gerado em um banco de dados que você acabou de restaurar de um backup, certifique-se de ter seguido as etapas descritas na documentação de backup e restauração, inclusive executando **sp_replrestart** , se apropriado. Para obter mais informações, consulte [Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
 Esse erro é um erro de processamento interno e, se for gerado em circunstâncias diferentes de uma restauração, geralmente indica que a replicação deve ser removida e reconfigurada. Se você não puder remover a replicação, entre em contato com o atendimento ao cliente para assistência técnica.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  
