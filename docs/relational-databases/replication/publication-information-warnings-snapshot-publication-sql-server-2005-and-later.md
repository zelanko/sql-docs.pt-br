---
title: "Informa&#231;&#245;es da Publica&#231;&#227;o, Avisos (publica&#231;&#227;o de instant&#226;neo, SQL Server 2005 e vers&#245;es posteriores) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1"
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Informa&#231;&#245;es da Publica&#231;&#227;o, Avisos (publica&#231;&#227;o de instant&#226;neo, SQL Server 2005 e vers&#245;es posteriores)
  A guia **Avisos** está disponível para Distribuidores que estão executando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A guia **Avisos** permite executar as seguintes tarefas para a publicação selecionada:  
  
-   Habilitar avisos.  
  
-   Especificar limites associados a avisos.  
  
-   Definir alertas associados a avisos.  
  
## Avisos, limites e alertas  
 Por padrão, o Replication Monitor exibe avisos para assinaturas não inicializadas: um status **Assinatura não inicializada** é exibido como um aviso na coluna **Status** de páginas que incluem informações de assinatura. Para publicações de instantâneo, você também pode especificar que a expiração iminente da assinatura resulte em um aviso, com a definição da opção **Avisar se uma assinatura for expirar dentro do limite**. Se o limite especificado for atingido ou excedido, o status da assinatura será exibido como **expirando em breve/expirado** (a menos que um problema com uma prioridade mais alta precise ser exibido).  
  
 Além de exibir de um aviso no Replication Monitor, atingir um limite também pode disparar um alerta. Os alertas são definidos clicando em **Configurar Alertas** e fornecendo informações na caixa de diálogo **Configurar Alertas de Replicação** .  
  
## Opções  
 **Ativado**  
 Selecione para habilitar um aviso e especificar um limite.  
  
 **Aviso**  
 Uma descrição do aviso associada a um limite.  
  
 **Limite**  
 Especifique um valor para o limite.  
  
 **Configurar Alertas**  
 Selecione uma linha no **avisos** grade e clique em **Configurar alertas** para iniciar o **Configurar alertas de replicação** caixa de diálogo. A caixa de diálogo permite definir um alerta associado ao limite selecionado e ao aviso.  
  
 **Descartar Alterações**  
 Clique para descartar qualquer alteração em avisos e limites.  
  
> [!NOTE]  
>  Clicar em **Descartar alterações** não afeta os alertas definidas no **Configurar alertas de replicação** caixa de diálogo.  
  
 **Salvar alterações**  
 Clique para salvar qualquer alteração em avisos e limites.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para uma publicação e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  