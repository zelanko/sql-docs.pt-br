---
title: "Segurança do Queue Reader Agent | Microsoft Docs"
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
- sql13.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 58afa56e66377ea4ac00bd9296128bbe7483719c
ms.lasthandoff: 04/11/2017

---
# <a name="queue-reader-agent-security"></a>Segurança do Agente de Leitor de Fila
  A caixa de diálogo **Segurança do Agente de Leitor de Fila** permite que você especifique a conta [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o Agente de Leitor de Fila executa e faz conexões locais com o Distribuidor. O agente se conecta ao Publicador usando a conta especificada na caixa de diálogo **Propriedades do Publicador** (disponível na caixa de diálogo **Propriedades do Distribuidor** ); o agente se conecta ao Assinante usando o mesmo contexto do Agente de Distribuição para a assinatura. Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 A conta deve ser válida, com a senha correta especificada. Contas e senhas não são validadas até que um agente seja executado.  
  
## <a name="options"></a>Opções  
 **Conta do processo**  
 Insira uma conta do Windows na qual o Agente de Leitor de Fila seja executado no Distribuidor. A conta do Windows especificada deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.  
  
 **Senha** e **Confirmar senha**  
 Insira a senha para a conta do Windows.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
