---
title: MSSQL_ENG024070 | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
caps.latest.revision: "14"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ccc818ae3ac140bb643fc4446faf93e16648935
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="mssqleng024070"></a>MSSQL_ENG024070
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|24070|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O cliente não possui o privilégio exigido.|  
  
## <a name="explanation"></a>Explicação  
 Este é um erro geral que pode ocorrer independentemente do uso de replicação. Para um servidor em uma topologia de replicação, geralmente o erro ocorre porque a conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é alterada usando o Gerenciador de Controle de Serviços do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows em vez do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Ao tentar executar um trabalho de agente após alterar a conta de serviço, pode ocorrer falha no trabalho com uma mensagem de erro semelhante à seguinte:  
  
 `Executed as user: \<UserAccount>. Replication-Replication Snapshot Subsystem: agent \<AgentName> failed. Executed as user: \<UserAccount>. A required privilege is not held by the client. The step failed. [SQLSTATE 42000] (Error 14151). The step failed.`  
  
 Esse problema ocorre porque o Gerenciador de Controle de Serviços do Windows não é capaz de conceder as permissões solicitadas para a nova conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="user-action"></a>Ação do usuário  
 Para evitar esse problema posteriormente, sempre use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager em vez do Gerenciador de Controle de Serviços do Windows para alterar as contas e as senhas de serviço.  
  
 Para resolver esse problema, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para alterar a conta de serviço de volta para a conta original. Em seguida, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para alterar para a nova conta. Ao fazer isso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager adiciona a nova conta ao seguinte grupo de segurança:  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 Ser um membro desse grupo de segurança concede à nova conta as permissões exigidas para executar o trabalho do agente de replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
