---
title: MSSQLSERVER_21893 | Microsoft Docs
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
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bf6c8b8f2ad46c1874a2b46fb74ec46c67d634c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118343"
---
# <a name="mssqlserver21893"></a>MSSQLSERVER_21893
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21893|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21893|  
|Texto da mensagem|Os assinantes (%s) do publicador original '%s' não aparecem como servidores remotos no publicador redirecionado '%s'. Execute `sp_addlinkedserver` no publicador redirecionado para adicionar esses assinantes como servidores remotos.|  
  
## <a name="explanation"></a>Explicação  
 `sp_validate_redirected_publisher` usa as tabelas de metadados de assinatura do banco de dados do publicador no servidor remoto para identificar seus assinantes associados e verifica se há entradas associadas em Master.dbo. sysservers para os assinantes. Este erro será retornado se algum assinante identificado não estiver presente.  
  
 Este erro não é considerado fatal. Os agentes que encontrarem este erro o registrará em log como erro informativo, mas não finalizarão, já que a falta entradas de assinante apropriadas no novo publicador limitou o impacto na replicação. Sem uma entrada apropriada para um assinante em sysservers, algumas atividades de gerenciamento de assinatura podem falhar quando executadas por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, essas mesmas atividades podem ser realizadas com êxito, executando explicitamente os procedimentos armazenados de gerenciamento.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute `sp_addlinkedserver` no publicador redirecionado para cada assinante identificado, a fim de adicioná-los como servidores remotos. Em seguida, execute `sp_serveroption` para definir o bit do assinante para o servidor.  
  
  