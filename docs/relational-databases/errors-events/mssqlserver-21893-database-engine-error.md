---
title: MSSQLSERVER_21893 | Microsoft Docs
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
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c4bd7053dc90563f163b2e53ee96d8bb72aa1b46
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver21893"></a>MSSQLSERVER_21893
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21893|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21893|  
|Texto da mensagem|Os assinantes (%s) do publicador original '%s' não aparecem como servidores remotos no publicador redirecionado '%s'. Execute **sp_addlinkedserver** no publicador redirecionado para adicionar esses assinantes como servidores remotos.|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_redirected_publisher** usa as tabelas de metadados de assinatura do banco de dados publicador no servidor remoto para identificar seus assinantes associados e verifica se há entradas associadas em master.dbo.sysservers para os assinantes. Este erro será retornado se algum assinante identificado não estiver presente.  
  
Este erro não é considerado fatal. Os agentes que encontrarem este erro o registrará em log como erro informativo, mas não finalizarão, já que a falta entradas de assinante apropriadas no novo publicador limitou o impacto na replicação. Sem uma entrada apropriada para um assinante em sysservers, algumas atividades de gerenciamento de assinatura podem falhar quando executadas por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, essas mesmas atividades podem ser realizadas com êxito, executando explicitamente os procedimentos armazenados de gerenciamento.  
  
## <a name="user-action"></a>Ação do usuário  
Execute **sp_addlinkedserver** no publicador redirecionado para cada assinante identificado, a fim de adicioná-los como servidores remotos. Em seguida, execute **sp_serveroption** para definir o bit do assinante para o servidor.  
  

