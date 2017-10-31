---
title: MSSQLSERVER_1401 | Microsoft Docs
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
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1968d85a421b61fa31dbe2a83c7f7773c8a89db0
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

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
[Iniciar, parar, pausar, retomar e reiniciar o Mecanismo de Banco de Dados, o SQL Server Agent ou o Serviço SQL Server Browser](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  

