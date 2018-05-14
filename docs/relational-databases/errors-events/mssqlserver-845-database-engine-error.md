---
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2d9b231b6cf2152e825b07dc1e3e218815d9df1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver845"></a>MSSQLSERVER_845
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|845|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|BUFLATCH_TIMEOUT|  
|Texto da mensagem|Tempo limite excedido ao aguardar pelo tipo de fechamento de buffer %d para página %S_PGID, da ID de banco de dados %d.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu uma falha; um processo estava aguardando para adquirir uma trava, mas o tempo limite expirou. Isso pode ocorrer se uma operação de E/S levar muito tempo para ser concluída, geralmente porque outras tarefas estão bloqueando os processos do sistema. Em algumas instâncias, esse erro pode ser o resultado de um problema de hardware.  
  
## <a name="user-action"></a>Ação do usuário  
Executar as seguintes tarefas pode evitar esse erro:  
  
-   Reduza a carga de trabalho.  
  
-   Verifique se há falhas de E/S associadas no log de erros ou no log de eventos. Geralmente, as falhas de E/S são causadas por funcionamento inadequado do disco.  
  
-   Verifique o log de erros de tarefas não produzidas e outros erros críticos.  
  
-   Se ocorrerem erros críticos frequentemente, como afirmações, resolva esses problemas.  
  
Se o erro persistir, contate o Serviço de Suporte e Atendimento ao Cliente Microsoft.  
  
