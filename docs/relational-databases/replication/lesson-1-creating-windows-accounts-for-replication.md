---
title: "Li&#231;&#227;o 1: Criando contas do Windows para replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicação [SQL Server], tutoriais"
  - "replicação [SQL Server], administrando"
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Li&#231;&#227;o 1: Criando contas do Windows para replica&#231;&#227;o
Nesta lição, você criará contas de Windows para executar os agentes de replicação. Você criará uma conta de Windows separada no servidor local para os seguintes agentes:  
  
|Agente|Local|Nome da conta|  
|---------|------------|----------------|  
|Snapshot Agent|Publicador|\<*machine_name*>\repl_snapshot|  
|Agente de Leitor de Log|Publicador|\<*machine_name*>\repl_logreader|  
|Agente de Distribuição|Publicador e assinante|\<*machine_name*>\repl_distribution|  
|Merge Agent|Publicador e assinante|\<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> Nos tutoriais de replicação, o Publicador e o Distribuidor compartilham a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Publicador e o Assinante podem compartilhar a mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso não é um requisito. Se o Publicador e o Assinante compartilharem a mesma instância, as etapas usadas para criar contas no Assinante não são necessárias.  
  
### Para criar contas locais do Windows local para agentes de replicação no Publicador  
  
1.  No Publicador, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e clique em **Novo Usuário**.  
  
4.  Insira **repl_snapshot** na caixa **Nome de usuário**, forneça a senha e outras informações relevantes e clique em **Criar** para criar uma conta repl_snapshot.  
  
5.  Repita a etapa anterior para criar as contas de repl_logreader, repl_distribution e repl_merge.  
  
6.  Clique em **Fechar**.  
  
### Para criar contas locais do Windows para agentes de replicação no Assinante  
  
1.  No Assinante, abra **Gerenciamento do Computador** em **Ferramentas Administrativas** no Painel de Controle.  
  
2.  Em **Ferramentas do Sistema**, expanda **Usuários e Grupos Locais**.  
  
3.  Clique com o botão direito do mouse em **Usuários** e clique em **Novo Usuário**.  
  
4.  Insira **repl_distribution** na caixa **Nome de usuário**, forneça a senha e outras informações relevantes e clique em **Criar** para criar uma conta repl_distribution.  
  
5.  Repita a etapa anterior para criar a conta de repl_merge.  
  
6.  Clique em **Fechar**.  
  
## Próximas etapas  
Você criou contas de Windows com sucesso para os agentes de replicação. A seguir, você configurará a pasta de instantâneo. Consulte [Lição 2: Preparando a pasta do instantâneo](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md).  
  
## Consulte também  
[Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
  
