---
title: MSSQL_ENG024070 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0b00aaa039da599c6a212645b9980df41d41d03f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85721589"
---
# <a name="mssql_eng024070"></a>MSSQL_ENG024070
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|24070|  
|Origem do Evento|MSSQLSERVER|  
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
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
