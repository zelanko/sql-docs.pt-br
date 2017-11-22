---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff486acfff1f68078e702ec792ecfc09aba006d5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8443|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB_DIALOG_WO_CONV_GROUP|  
|Texto da mensagem|A conversa com a ID '%.*ls' e o iniciador %d referencia um grupo de conversa ausente '%.\*ls'. Execute DBCC CHECKDB para analisar e reparar o banco de dados.|  
  
## <a name="explanation"></a>Explicação  
A camada de metadados retornou NULL para o grupo de conversa. O banco de dados foi corrompido de algum modo. Uma possível origem da corrupção é um erro de disco.  
  
## <a name="user-action"></a>Ação do usuário  
Execute DBCC CHECKDB no modo de correção para deixar novamente o banco de dados em um estado consistente. É possível excluir mensagens, se necessário, para restaurar a consistência. Investigue os logs de erros do sistema para saber se o erro foi causado por outra falha no sistema.  
  
