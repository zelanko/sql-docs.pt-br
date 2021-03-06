---
description: Segurança do Agente &lt;AgentName&gt;
title: Segurança do Agente &lt;AgentName&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: dda2486c57ce61bb29774bf44cf01265c39864a7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467337"
---
# <a name="ltagentnamegt-agent-security"></a>Segurança do Agente &lt;AgentName&gt;
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  A página **Segurança do agente \<AgentName>** permite especificar as contas nas quais o Agente de Distribuição (para replicação transacional ou de instantâneo) ou o Agente de Mesclagem (para replicação de mesclagem) é executado e faz conexões com os computadores em uma topologia de replicação. Para obter informações sobre as permissões necessárias para os agentes e as melhores práticas de segurança da replicação, consulte [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md) e [Melhores práticas de segurança da replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opções  
 Clique no botão de propriedades ( **...** ) na linha de cada Assinante para acessar a caixa de diálogo **Segurança do Distribution Agent** ou **Segurança do Merge Agent** . Clique em **Ajuda** na caixa de diálogo que é iniciada para obter mais informações sobre as permissões requeridas para contas usadas pelos agentes.  
  
 Depois que as configurações forem inseridas em uma das caixas de diálogo, as informações de conexão para o Assinante serão exibidas na grade.  
  
 **Agente para Assinante**  
 O nome de cada Assinante.  
  
 **Conexão com o Distribuidor**  
 Exibido para replicação de instantâneo e transacional. O contexto no qual a conexão com o Distribuidor é feita. Conexões locais sempre são feitas usando o contexto de conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no qual o agente executa:  
  
-   Para assinaturas push, a conexão local é a conexão com o Distribuidor, portanto, esse campo sempre exibirá: **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** para assinaturas push.  
  
-   Para assinaturas pull, a conexão pode ser feita também no contexto de um logon [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O campo exibe uma das opções a seguir: **Usar o logon '\<Login>'** , **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** . A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
 **Conexão com o Publicador e Distribuidor**  
 Exibido para replicação de mesclagem. O contexto no qual as conexões com o Publicador e o Distribuidor são feitas. Conexões locais sempre são feitas usando o contexto da conta do Windows na qual o agente é executado:  
  
-   Para assinaturas push, a conexão local é a conexão com o Editor e o Distribuidor, portanto, esse campo sempre exibirá: **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** para assinaturas push.  
  
-   Para assinaturas pull, a conexão pode ser feita também no contexto de um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe uma das opções a seguir: **Usar o logon '\<Login>'** , **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** . A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
 **Conexão com o Assinante**  
 O contexto no qual a conexão com o Assinante é feita. Conexões locais sempre são feitas usando o contexto da conta do Windows na qual o agente é executado:  
  
-   Para assinaturas pull, a conexão local é a conexão com o Assinante, portanto, esse campo sempre exibirá: **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** para assinaturas push.  
  
-   Para assinaturas push, a conexão pode ser feita também no contexto de um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe uma das opções a seguir: **Usar o logon '\<Login>'** , **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** . A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Controle de acesso e identidade para replicação](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
