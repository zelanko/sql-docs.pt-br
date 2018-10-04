---
title: Categoria de evento de auditoria de segurança | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d52589fc39376d5dfdfa3f540d3d1d47e89f448
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224230"
---
# <a name="security-audit-event-category"></a>Categoria de evento de auditoria de segurança
  A categoria de evento de auditoria de segurança tem as classes de evento descritas na tabela a seguir.  
  
|Event Class|ID do evento|Description|  
|-----------------|--------------|-----------------|  
|Audit Login|1|Registra todos os novos eventos de conexão desde o início do rastreamento, por exemplo, quando um cliente solicitou uma conexão a um servidor que executa uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|Audit Logout|2|Registra todos os novos eventos de desconexão desde o início do rastreamento, como quando um cliente emite um comando de desconexão.|  
|Audit Server Starts and Stops|4|Registra as atividades de desligamento, inicialização e pausa dos serviços.|  
|Audit Object Permission Event|18|Registra todas as alterações de permissão de objeto.|  
|Evento de Operações de Administração de Auditoria|19|Registra operações de servidor para fazer backup, restaurar, sincronizar, anexar, desanexar, carregar e salvar imagem.|  
  
 Para obter informações sobre as colunas associadas a cada classe de evento de auditoria de segurança, consulte [Colunas de dados de auditoria de segurança](security-audit-data-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Eventos de rastreamento do Analysis Services](analysis-services-trace-events.md)  
  
  
