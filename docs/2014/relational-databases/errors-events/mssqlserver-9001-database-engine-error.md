---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c1b57637cee601cde328bc079ab907629591b5f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019180"
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
  
  