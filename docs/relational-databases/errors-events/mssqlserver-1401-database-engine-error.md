---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: fdae41b3011a31be94777a9ffc05dd9304d0f315
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1401|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_MASTERSTARTUP|  
|Texto da mensagem|Falha na inicialização da rotina de thread mestre do espelhamento de banco de dados pelo seguinte motivo: %ls. Corrija a causa do erro e reinicialize o serviço SQL Server.|  
  
## <a name="explanation"></a>Explicação  
Falha na inicialização do thread de controle de espelhamento.  
  
## <a name="user-action"></a>Ação do usuário  
No log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], procure o erro associado que precedeu essa mensagem. Corrija a causa do erro e reinicie o serviço (MSSQLSERVER) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
[Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
