---
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce297a1c2bc782a82a322618acedb102bb9e18eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101490"
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
  
