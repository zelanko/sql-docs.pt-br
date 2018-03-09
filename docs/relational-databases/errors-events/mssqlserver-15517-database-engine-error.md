---
title: MSSQLSERVER_15517 | Microsoft Docs
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
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d35b694fdb0f27bbbe3cabc9c36df66553e4c87
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver15517"></a>MSSQLSERVER_15517
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|15517|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CANNOTEXECUTEASUSER|  
|Texto da mensagem|Não é possível executar como banco de dados de entidade, pois a entidade “*principal*” não existe, esse tipo de entidade não pode ser representada ou você não tem permissão para isso.|  
  
## <a name="user-action"></a>Ação do usuário  
Use o nome de uma entidade existente ou obtenha a permissão IMPERSONATE nessa entidade.  
  
15517 também pode ocorrer depois da execução de um anexo e a restauração de um banco de dados por alguém que não seja o proprietário original do banco de dados. Para resolver esse erro, altere o db_owner para um logon no servidor, executando o seguinte comando:  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>Consulte também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
