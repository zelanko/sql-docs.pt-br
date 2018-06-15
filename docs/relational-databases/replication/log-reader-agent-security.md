---
title: Segurança do Agente de Leitor de Log | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.LRA.f1
helpviewer_keywords:
- Log Reader Agent Security dialog box
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d846aafbd1aacc77d9cec9d2de311779284a8426
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32957841"
---
# <a name="log-reader-agent-security"></a>Segurança do Log Reader Agent
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A caixa de diálogo **Segurança do Log Reader Agent** permite especificar:  
  
-   A conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o Log Reader Agent é executado no Distribuidor. A conta do Windows é também referida como *conta do processo*, porque o processo do agente é executado nessa conta.  
  
-   O contexto no qual o Log Reader Agent faz conexões com o Editor [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A conexão pode ser feita representando a conta do Windows ou no contexto de uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada por você.  
  
    > [!NOTE]  
    >  O Log Reader Agent fará conexões com o Publicador mesmo que o Publicador e o Distribuidor estejam no mesmo computador. O Log Reader Agent também faz conexões com o Distribuidor; essas conexões sempre são feitas representando a conta do Windows na qual o agente é executado.  
  
     Para Publicadores Oracle, especifique o contexto no qual o Log Reader Agent faz conexão com o Editor na caixa de diálogo **Propriedades do Publicador** (disponível na caixa de diálogo **Propriedades do Distribuidor** ). Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Todas as contas devem ser válidas, com a senha correta especificada para cada conta. Contas e senhas não são validadas até que um agente seja executado.  
  
## <a name="options"></a>Opções  
 **Conta do processo**  
 Insira uma conta do Windows na qual o Log Reader Agent é executado no Distribuidor. A conta do Windows especificada deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.  
  
 **Senha** e **Confirmar Senha**  
 Insira a senha para a conta do Windows.  
  
 **Conectar ao Publicador**  
 Selecione se o Log Reader Agent deverá fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta de processo** ou usando uma conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para conexão com o Assinante deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
