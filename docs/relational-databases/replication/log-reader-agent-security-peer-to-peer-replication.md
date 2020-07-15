---
title: Segurança do Agente de Leitor de Log (SSMS)
description: Descreve a página 'Segurança do Agente de Leitor de Log' de uma transação e uma publicação ponto a ponto do SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ef28a7831ad5d4c63b450da177037d55534b5f63
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716768"
---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>Segurança do Agente de Leitor de Log (replicação ponto a ponto)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  A página **Segurança do Agente de Leitor de Log** permite especificar as contas nas quais o Agente de Leitor de Log, em cada computador de mesmo nível, executa e efetua conexões. Para obter informações sobre as permissões necessárias para os agentes e as melhores práticas de segurança da replicação, consulte [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md) e [Melhores práticas de segurança da replicação](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Há um Agente de Leitor de Log para cada banco de dados publicado que usa a replicação transacional. Se o Agente de Leitor de Log de um banco de dados já foi configurado (para uma publicação em uma execução anterior desse assistente ou para outra publicação transacional no mesmo banco de dados), você não poderá trocar as credenciais que ele usa nesse assistente. Se você especificar credenciais novas, elas serão ignoradas. Para alterar credenciais, use a caixa de diálogo **Propriedades de Publicação** . Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Opções  
 Clique no botão de propriedades ( **...** ) na linha de cada computador par para acessar a caixa de diálogo **Segurança do Agente de Leitor de Log** . Clique em **Ajuda** na caixa de diálogo **Segurança do Agente de Leitor de Log** iniciada, para obter mais informações sobre as permissões necessárias para as contas usadas pelos agentes.  
  
 Depois que as configurações forem inseridas na caixa de diálogo, serão exibidas informações de conexão para o Assinante na grade.  
  
 **Agentes para o Publicador**  
 O nome de cada instância de servidor de computador par.  
  
 **Banco de dados par**  
 O banco de dados que serve como banco de dados de publicação e banco de dados de assinatura em cada nível.  
  
 **Conexão com o Distribuidor**  
 O contexto no qual a conexão com o Distribuidor é feita. A conexão local com o Distribuidor é sempre feita usando o contexto da conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado e, portanto, esse campo sempre exibirá **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** .  
  
 **Conexão com o Publicador**  
 O contexto no qual a conexão com o Publicador é feita. A conexão com o Publicador pode ser feita usando um logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o contexto de uma conta do Windows na qual o agente é executado. O campo exibe uma das opções a seguir: **Usar o logon '\<Login>'** , **Representar '\<Domain>\\<Logon\>'** ou **Representar '\<Computer>\\<Logon\>'** . A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que todas as conexões sejam feitas com o uso do contexto da conta do Windows.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar uma topologia ponto a ponto &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
