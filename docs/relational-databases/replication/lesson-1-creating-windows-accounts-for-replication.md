---
title: "Lição 1: Criando contas do Windows para replicação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
- replication [SQL Server], administering
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 606bcbead7c379fa3fe54bd975e683adfca857cc
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="lesson-1-creating-windows-accounts-for-replication"></a>Lição 1: Criando contas do Windows para replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Nesta lição, você criará contas de Windows para executar os agentes de replicação. Você criará uma conta de Windows separada no servidor local para os seguintes agentes:  
  
|Agente|Local|Nome da conta|  
|---------|------------|----------------|  
|Snapshot Agent|Publicador|\<*machine_name*>\repl_snapshot|  
|Agente de Leitor de Log|Publicador|\<*machine_name*>\repl_logreader|  
|Agente de Distribuição|Publicador e assinante|\<*machine_name*>\repl_distribution|  
|Agente de Mesclagem|Publicador e assinante|\<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> Nos tutoriais de replicação, o Publicador e o Distribuidor compartilham a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Publicador e o Assinante podem compartilhar a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso não é um requisito. Se o Publicador e o Assinante compartilharem a mesma instância, as etapas usadas para criar contas no Assinante não são necessárias.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Para criar contas locais do Windows local para agentes de replicação no Publicador  
  
1.  No Publicador, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e clique em **Novo Usuário**.  
  
4.  Insira **repl_snapshot** na caixa **Nome de usuário** , forneça a senha e outras informações relevantes e clique em **Criar** para criar uma conta repl_snapshot.  
  
5.  Repita a etapa anterior para criar as contas de repl_logreader, repl_distribution e repl_merge.  
  
6.  Clique em **Fechar**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>Para criar contas locais do Windows para agentes de replicação no Assinante  
  
1.  No Assinante, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e clique em **Novo Usuário**.  
  
4.  Insira **repl_distribution** na caixa **Nome de usuário** , forneça a senha e outras informações relevantes e clique em **Criar** para criar uma conta repl_distribution.  
  
5.  Repita a etapa anterior para criar a conta de repl_merge.  
  
6.  Clique em **Fechar**.  
  
## <a name="next-steps"></a>Next Steps  
Você criou contas de Windows com sucesso para os agentes de replicação. A seguir, você configurará a pasta de instantâneo. Consulte [Lição 2: Preparando a pasta do instantâneo](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Consulte Também  
[Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
  
