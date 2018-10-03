---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23dc13b8dac23914cc4f337e4b39fbf84ee4b782
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47700974"
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
