---
title: Segurança do Agente &lt;AgentName&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d77f8d6acb449bc9aa2298dbcba9782fd7bc07e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722048"
---
# <a name="ltagentnamegt-agent-security"></a>Segurança do Agente &lt;AgentName&gt;
  A página **Segurança do agente \<AgentName>** permite especificar as contas nas quais o Agente de Distribuição (para replicação transacional ou de instantâneo) ou o Agente de Mesclagem (para replicação de mesclagem) é executado e faz conexões com os computadores em uma topologia de replicação. Para obter informações sobre as permissões necessárias para os agentes e as melhores práticas de segurança da replicação, consulte [Modelo de segurança do agente de replicação](security/replication-agent-security-model.md) e [Melhores práticas de segurança da replicação](security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opções  
 Clique no botão de propriedades (**...**) na linha de cada Assinante para acessar a caixa de diálogo **Segurança do Distribution Agent** ou **Segurança do Merge Agent** . Clique em **Ajuda** na caixa de diálogo que é iniciada para obter mais informações sobre as permissões requeridas para contas usadas pelos agentes.  
  
 Depois que as configurações forem inseridas em uma das caixas de diálogo, as informações de conexão para o Assinante serão exibidas na grade.  
  
 **Agente para Assinante**  
 O nome de cada Assinante.  
  
 **Conexão com o Distribuidor**  
 Exibido para replicação de instantâneo e transacional. O contexto no qual a conexão com o Distribuidor é feita. Conexões locais sempre são feitas usando o contexto de conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no qual o agente executa:  
  
-   Para assinaturas push, a conexão local é a conexão com o Distribuidor, portanto, esse campo sempre exibirá: **Representar '\<Domínio>\\<Logon\>'** ou **Representar '\<Computador>\\<Logon\>'** para assinatura push.  
  
-   Para assinaturas pull, a conexão pode ser feita também no contexto de um logon [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe uma das opções a seguir: **Use logon '\<Logon>'**, **Representar '\<Domínio>\\<Logon\>'** ou **Representar '\<Computador>\\<Logon\>'**. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
 **Conexão com o Publicador e Distribuidor**  
 Exibido para replicação de mesclagem. O contexto no qual as conexões com o Publicador e o Distribuidor são feitas. Conexões locais sempre são feitas usando o contexto da conta do Windows na qual o agente é executado:  
  
-   Para assinaturas push, a conexão local é a conexão com o Editor e o Distribuidor, portanto, esse campo sempre exibirá: **Representar '\<Domínio>\\<Logon\>'** ou **Representar '\<Computador>\\<Logon\>'** para assinatura push.  
  
-   Para assinaturas pull, a conexão pode ser feita também no contexto de um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe uma das opções a seguir: **Use logon '\<Logon>'**, **Representar '\<Domínio>\\<Logon\>'** ou **Representar '\<Computador>\\<Logon\>'**. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
 **Conexão com o Assinante**  
 O contexto no qual a conexão com o Assinante é feita. Conexões locais sempre são feitas usando o contexto da conta do Windows na qual o agente é executado:  
  
-   Para assinaturas pull, a conexão local é a conexão com o Assinante, portanto, esse campo sempre exibirá: **Representar '\<Domínio>\\<Logon\>'** ou **Representar '\<Computador>\\<Logon\>'** para assinatura push.  
  
-   Para assinaturas push, a conexão pode ser feita também no contexto de um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O campo exibe uma das opções a seguir: **Use logon '\<Logon>'**, **Representar '\<Domínio>\\<Logon\>'** ou **Representar '\<Computador>\\<Logon\>'**. A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de assinatura pull](view-and-modify-pull-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura push](view-and-modify-push-subscription-properties.md)   
 [Gerenciar logons e senhas na replicação](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modelo de segurança do agente de replicação](security/replication-agent-security-model.md)   
 [Segurança de replicação do SQL Server](security/view-and-modify-replication-security-settings.md)  
  
  
