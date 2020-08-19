---
description: Segurança do Agente de Leitor de Fila
title: Segurança do Queue Reader Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dc5a8ff1f69f26fc7925a2314151e9437ffefc65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88406242"
---
# <a name="queue-reader-agent-security"></a>Segurança do Agente de Leitor de Fila
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  A caixa de diálogo **Segurança do Agente de Leitor de Fila** permite que você especifique a conta [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o Agente de Leitor de Fila executa e faz conexões locais com o Distribuidor. O agente se conecta ao Publicador usando a conta especificada na caixa de diálogo **Propriedades do Publicador** (disponível na caixa de diálogo **Propriedades do Distribuidor** ); o agente se conecta ao Assinante usando o mesmo contexto do Agente de Distribuição para a assinatura. Para obter mais informações, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 A conta deve ser válida, com a senha correta especificada. Contas e senhas não são validadas até que um agente seja executado.  
  
## <a name="options"></a>Opções  
 **Conta do processo**  
 Insira uma conta do Windows na qual o Agente de Leitor de Fila seja executado no Distribuidor. A conta do Windows especificada deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.  
  
 **Senha** e **Confirmar Senha**  
 Insira a senha para a conta do Windows.  
  
## <a name="see-also"></a>Consulte Também  
 [Controle de acesso e identidade para replicação](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
