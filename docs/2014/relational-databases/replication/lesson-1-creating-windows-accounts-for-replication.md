---
title: 'Lição 1: Criando contas do Windows para replicação | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
- replication [SQL Server], administering
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a3bd3b0369c990b6db3dc1cbb44f7fd387289ce9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303646"
---
# <a name="lesson-1-creating-windows-accounts-for-replication"></a>Lição 1: Criando contas do Windows para replicação
  Nesta lição, você criará contas de Windows para executar os agentes de replicação. Você criará uma conta de Windows separada no servidor local para os seguintes agentes:  
  
|Agente|Local|Nome da conta|  
|-----------|--------------|------------------|  
|Snapshot Agent|Publicador|\<*machine_name*>\repl_snapshot|  
|Agente de Leitor de Log|Publicador|\<*machine_name*>\repl_logreader|  
|Agente de Distribuição|Publicador e assinante|\<*machine_name*>\repl_distribution|  
|Agente de Mesclagem|Publicador e assinante|\<*machine_name*>\repl_merge|  
  
> [!NOTE]  
>  Nos tutoriais de replicação, o Publicador e o Distribuidor compartilham a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Publicador e o Assinante podem compartilhar a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso não é um requisito. Se o Publicador e o Assinante compartilharem a mesma instância, as etapas usadas para criar contas no Assinante não são necessárias.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Para criar contas locais do Windows local para agentes de replicação no Publicador  
  
1.  No Publicador, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e clique em **Novo Usuário**.  
  
4.  Insira `repl_snapshot` no **nome de usuário** caixa, forneça a senha e outras informações relevantes e, em seguida, clique em **criar** para criar uma conta repl_snapshot.  
  
5.  Repita a etapa anterior para criar as contas de repl_logreader, repl_distribution e repl_merge.  
  
6.  Clique em **Fechar**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>Para criar contas locais do Windows para agentes de replicação no Assinante  
  
1.  No Assinante, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e clique em **Novo Usuário**.  
  
4.  Insira `repl_distribution` no **nome de usuário** caixa, forneça a senha e outras informações relevantes e, em seguida, clique em **criar** para criar uma conta repl_distribution.  
  
5.  Repita a etapa anterior para criar a conta de repl_merge.  
  
6.  Clique em **Fechar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você criou contas de Windows com sucesso para os agentes de replicação. A seguir, você configurará a pasta de instantâneo. Consulte [Lição 2: Preparando a pasta do instantâneo](lesson-2-preparing-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos agentes de replicação.](agents/replication-agents-overview.md)  
  
  
