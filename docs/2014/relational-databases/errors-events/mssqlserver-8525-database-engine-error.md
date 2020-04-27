---
title: MSSQLSERVER_8525 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0e254e38eabc62ab3e11e7d8ab1a3396c465470
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62913231"
---
# <a name="mssqlserver_8525"></a>MSSQLSERVER_8525
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8525|  
|Origem do Evento|MSSQLSERVER|  
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
  
  
