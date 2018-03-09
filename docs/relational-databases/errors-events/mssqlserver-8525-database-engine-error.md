---
title: MSSQLSERVER_8525 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a573b27b2d0a86a2e6a5d6634005f463b888c59
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver8525"></a>MSSQLSERVER_8525
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8525|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Transação distribuída concluída. Inscreva esta sessão em uma transação nova ou na transação NULL.|  
  
## <a name="explanation"></a>Explicação  
O modelo de programação para usar o Coordenador de Transações Distribuídas com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que os aplicativos sejam explicitamente inscritos e removidos de uma transação distribuída.  
  
Este erro acontece quando as quatro condições seguintes são cumpridas:  
  
-   O aplicativo foi inscrito em uma transação distribuída.  
  
-   A transação terminou, foi confirmada ou revertida, por alguma razão.  
  
-   O aplicativo de usuário não foi explicitamente removido de uma transação distribuída nem foi explicitamente inscrito em uma nova transação distribuída.  
  
-   O aplicativo tenta fazer alguma operação transacional diferente de remover-se de uma transação distribuída existente ou de inscrever-se em uma nova transação distribuída, como emitir uma consulta ou iniciar uma transação local.  
  
O estado do erro 1 é usado quando o aplicativo executa uma operação que cria transações locais, e o estado do erro 2 é usado quando aplicativo tenta se inscrever em uma sessão associada.  
  
## <a name="user-action"></a>Ação do usuário  
Depois de um aplicativo inscrever-se em uma transação distribuída, o aplicativo deve ser removido explicitamente da transação distribuída ou deve ser inscrito em outra transação distribuída. Isto irá removê-lo implicitamente de uma transação inscrita anterior. Para a sintaxe exata para remoção ou inscrição em uma transação distribuída, consulte o manual de programação de interface do aplicativo.  
  
