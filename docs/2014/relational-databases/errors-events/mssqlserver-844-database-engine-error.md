---
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 55ab248466e7552f1265b047c559ca397d204148
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053621"
---
# <a name="mssqlserver_844"></a>MSSQLSERVER_844
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|844|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|BUFLATCH_TIMEOUT_CONTINUE|  
|Texto da mensagem|Tempo limite excedido ao aguardar a trava do buffer - tipo %d, bp %p, página %d:%d, stat %#x, id do banco de dados %d; id da unidade de alocação: %I64d%ls, tarefa 0x%p: %d, tempo de espera %d, sinalizadores 0x%I64x, tarefa proprietária 0x%p.  Continuando espera.|  
  
## <a name="explanation"></a>Explicação  
 Um processo está aguardando travamento. Esse problema pode ser causado por uma operação de E/S que leva muito tempo para ser concluída. Normalmente esse tipo de erro é o resultado de outros processos do sistema de bloqueio de tarefas. Em algumas instâncias, esse erro pode ser o resultado de um problema de hardware.  
  
## <a name="user-action"></a>Ação do usuário  
 Tente o seguinte para evitar que esse erro ocorra:  
  
-   Reduza a carga de trabalho.  
  
-   Verifique se há falhas de E/S associadas no log de erros ou no log de eventos. Normalmente as falhas de E/S indicam um funcionamento inadequado do disco.  
  
-   Verifique no log de erros se existem tarefas não produzidas e outros erros críticos.  
  
-   Se ocorrerem erros críticos frequentemente, como afirmações, resolva esses problemas.  
  
 Se o erro persistir, contate o Serviço de Suporte e Atendimento ao Cliente Microsoft.  
  
  
