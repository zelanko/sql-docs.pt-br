---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a0ea81464154aff79cd31a73871702d5110b1ce1
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968006"
---
# <a name="mssqlserver_1401"></a>MSSQLSERVER_1401
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1401|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_MASTERSTARTUP|  
|Texto da mensagem|Falha na inicialização da rotina de thread mestre do espelhamento de banco de dados pelo seguinte motivo: %ls. Corrija a causa do erro e reinicialize o serviço SQL Server.|  
  
## <a name="explanation"></a>Explicação  
 Falha na inicialização do thread de controle de espelhamento.  
  
## <a name="user-action"></a>Ação do usuário  
 No log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], procure o erro associado que precedeu essa mensagem. Corrija a causa do erro e reinicie o serviço (MSSQLSERVER) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
