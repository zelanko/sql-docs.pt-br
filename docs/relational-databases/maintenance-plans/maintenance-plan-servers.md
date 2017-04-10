---
title: "Plano de manuten&#231;&#227;o (Servidores) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.maint.servers.f1"
  - "sql13.swb.maint.maintplanproperties.server.f1"
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# Plano de manuten&#231;&#227;o (Servidores)
  Use a caixa de diálogo **Servidores** para selecionar os servidores em que você quer executar o plano de manutenção.  
  
 É necessário configurar um ambiente multisservidor contendo um servidor mestre e um ou mais servidores de destino para criar um plano de manutenção multisservidor. Para planos de manutenção multisservidor, o servidor local deve ser configurado como um servidor mestre. Em ambientes multisservidor, essa caixa de diálogo exibe o servidor mestre **(local)** e todos os servidores de destino correspondentes. Um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é criado para o servidor local. Ele está habilitado ou desabilitado dependendo se o servidor **(local)** for selecionado. Se os servidores de destino estiverem selecionados, um trabalho multisservidor será criado e baixado para cada um dos servidores de destino selecionados. Se nenhum servidor de destino estiver selecionado, o trabalho multisservidor será excluído.  
  
## Consulte também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md)   
 [Criar um servidor mestre](../../ssms/agent/make-a-master-server.md)   
 [Criar um servidor de destino](../../ssms/agent/make-a-target-server.md)  
  
  