---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cfc717c63cb85207315d00ae8dc06fdd881a503c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912435"
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
  
  
