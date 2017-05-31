---
title: "Segurança do Snapshot Agent | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.security.SSA.f1
helpviewer_keywords:
- Snapshot Agent Security dialog box
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a3834548fba6eb52e57836eefdb9f8917cb35d0
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="snapshot-agent-security"></a>Segurança do Snapshot Agent
  A caixa de diálogo **Segurança do Snapshot Agent** permite specificar:  
  
-   A conta [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o Snapshot Agent é executado no Distribuidor. A conta do Windows é também referida como *conta do processo*, porque o processo do agente é executado nessa conta.  
  
-   O contexto no qual o SnapshotAgent faz conexões com o Editor [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A conexão pode ser feita representando a conta do Windows ou no contexto de uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada por você.  
  
    > [!NOTE]  
    >  O Snapshot Agent faz conexões com o Editor mesmo que o Publicador e o Distribuidor estejam no mesmo computador. O Snapshot Agent também faz conexões com o Distribuidor; essas conexões são sempre feitas representando a conta do Windows na qual o agente é executado.  
  
     Para Editores Oracle, especifique o contexto no qual o Snapshot Agent faz conexão com o Publicador na caixa de diálogo **Propriedades do Publicador** (disponível na caixa de diálogo **Propriedades do Distribuidor** ). Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Todas as contas devem ser válidas, com a senha correta especificada para cada conta. Contas e senhas não são validadas até que um agente seja executado.  
  
## <a name="options"></a>Opções  
 **Process account**  
 Insira uma conta  Windows na qual o Snapshot Agent é executado no Distribuidor. A conta do Windows especificada deve:  
  
-   Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.  
  
-   Ter permissões de gravação no compartilhamento de instantâneo.  
  
 **Senha** e **Confirmar senha**  
 Insira a senha para a conta do Windows.  
  
 **Conectar ao Publicador**  
 Selecione se o Snapshot Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta de processo** ou usando uma conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  É recomendável a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para conexão com o Assinante deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de publicação.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
