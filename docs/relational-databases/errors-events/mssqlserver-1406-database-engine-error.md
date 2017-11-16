---
title: MSSQLSERVER_1406 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 543a02aceaaed5e6398d7b9e54b3918cc720d683
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1406"></a>MSSQLSERVER_1406
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1406|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_BADSTATEFORFORCESERVICE|  
|Texto da mensagem|Não foi possível forçar o serviço com segurança. Remova o espelhamento de banco de dados e recupere o banco de dados "%.*ls" para obter acesso.|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode forçar o serviço porque o estado de espelhamento não pode garantir que o processo forçar serviço funcione corretamente.  
  
## <a name="user-action"></a>Ação do usuário  
Remova o espelhamento de banco de dados. Depois, você pode recuperar o banco de dados espelho para obter acesso a ele.  
  
## <a name="see-also"></a>Consulte também  
[Forçar serviço em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](~/database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
[Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
