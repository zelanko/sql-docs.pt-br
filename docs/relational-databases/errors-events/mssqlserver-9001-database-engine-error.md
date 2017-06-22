---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1eaae857105a13a133c2fc9cd216d701df9f51d5
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9001|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOG_NOT_AVAIL|  
|Texto da mensagem|O log para o banco de dados '%.*ls' não está disponível. Verifique o log de eventos para obter as mensagens de erro relacionadas. Resolva todos os erros e reinicie o banco de dados.|  
  
## <a name="explanation"></a>Explicação  
O log do banco de dados foi colocado offline. Geralmente, isso indica uma falha catastrófica que exige reinicialização do banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
Analise os outros erros e reinicie a instância do SQL Server, caso ela ainda não tenha sido reinicializada.  
  

