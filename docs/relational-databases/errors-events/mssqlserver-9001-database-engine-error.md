---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 228db710fffb79e9fb799d8a14125b2febe6611b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791094"
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
